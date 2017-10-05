```Assembly   
File  Edit  Edit_Settings  Menu  Utilities  Compilers  Test  Help            
 sssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss
 EDIT       CSU0014.C3121.ASM(PROG6) - 01.99                Columns 00001 00072 
 Command ===>                                                  Scroll ===> CSR  
 ****** ***************************** Top of Data ******************************
 ==MSG> -CAUTION- Profile changed to NUMBER ON STD (from NUMBER OFF).           
 ==MSG>           Data has valid standard numbers.                              
 ==MSG> -CAUTION- Profile changed to CAPS ON (from CAPS OFF) because the        
 ==MSG>           data does not contain any lower case characters.              
 000100 //CSU0014A JOB (ASM),'C3121',CLASS=A,MSGCLASS=A,NOTIFY=&SYSUID,         
 000200 //   MSGLEVEL=(0,0),TIME=(,2),COND=(4,LT)                               
 000300 //****************************************************************      
 000400 //*   NEXT TWO PARAMETERS MUST BE SET BEFORE COMPILES!           *      
 000500 //****************************************************************      
 000600 //        SET   ID=14                                                   
 000700 //        SET   PROG=6                                                  
 000800 //****************************************************************      
 000900 //ASM    EXEC   PROC=HLASMCLG                                           
 001000 //SYSIN    DD   *                                                       
 001100          TITLE  'SKELETON ASSEMBLER PROGRAM'                            
 001200          PRINT  ON,NODATA,NOGEN                                         
 001300 ******************************************************************
 001400 *                                                                *      
 001500 *   PROGRAMMER:  DAVID WOOLBRIGHT                                *      
 001600 *   COMMENTS  :  ASM SKELETON PROGRAM                            *      
 001700 *                                                                *      
 001800 ******************************************************************      
 001900 *   STANDARD BEGINNING FOR ASSEMBLER PROGRAMS                    *      
 002000 ******************************************************************      
 002100 PROG6    CSECT                                                          
 002200          STM   R14,R12,12(R13)         STORE EXISTING REGISTERS         
 002300          LR    R12,R15                 ESTABLISH 1ST BASE REG           
 002400          USING PROG6,R12,R11,R10       DEFINING THREE BASE REGS         
 002500          LAY   R11,PROG6+4096          SECOND BASE REG + 4K             
 002600          LAY   R10,PROG6+8192          THIRD BASE REG + 8K              
 002700          ST    R13,SAVEAREA+4          BACKWARD CHAIN CALLER'S          
 002800          LA    R13,SAVEAREA            ADDRESS OF MY SAVE AREA          
 002900 ******************************************************************      
 003000 * BEGIN THE PROGRAM LOGIC. FIRST OPEN THE INPUT AND OUTPUT FILES *      
 003100 ******************************************************************
 003200          OPEN  (FILEIN1,(INPUT))      OPEN INPUT FILE                   
 003300          OPEN  (FILEOUT1,(OUTPUT))    OPEN OUTPUT FILE                  
 003400 *        PUT   FILEOUT1,PRHEAD         OUTPUT THE HEADER                
 003500          GET   FILEIN1,RECIN1          GET THE FIRST RECORD, IF ONE     
 003600 ******************************************************************      
 003700 *        READ AND PRINT LOOP                                     *      
 003800 ******************************************************************      
 003900 LOOP     EQU   *                                                        
 004000          PUT   FILEOUT1,CLEAR                                           
 004100          PUT   FILEOUT1,PRHEAD                                          
 004200          AP    RECOUNT,PK1             INCREMENT RECORD COUNT           
 004300          MVC   RECOUT1,CLEAR                                            
 004400          BAS   R8,SETUP                                                 
 004500          BAS   R8,CALC                                                  
 004600          BAS   R8,PRTLAST                                               
 004700          BAS   R8,PRTTOT                                                
 004800          GET   FILEIN1,RECIN1                                           
 004900          B     LOOP                    GO BACK AND PROCESS              
 005000 ******************************************************************      
 005100 *        END OF INPUT PROCESSING                                 *      
 005200 ******************************************************************      
 005300 EOF1     EQU   *                                                        
 005400          CLOSE (FILEIN1)               CLOSE INPUT FILE                 
 005500          CLOSE (FILEOUT1)              CLOSE OUTPUT FILE                
 005600          L     R13,SAVEAREA+4          POINT AT OLD SAVE AREA           
 005700          LM    R14,R12,12(R13)         RESTORE THE REGISTERS            
 005800          LA    R15,0                   RETURN CODE = 0                  
 005900          BR    R14                                                      
 006000 ******************************************************************      
 006100 *      PACK NUMBERS AND PRINT INITIAL HEADING                    *      
 006200 ******************************************************************      
 006300 SETUP    EQU   *                                                        
 006400          PACK  PKLN,LNAMT                                               
 006500          PACK  PKRATE,INTRATE                                           
 006600          PACK  PKPAY,PAYMENT                                            
 006700          PACK  PKTERM,TERM 
 006800          ZAP   TOTPAY,=PL1'0'                                           
 006900          ZAP   TOTINT,=PL1'0'                                           
 007000          ZAP   TOTPRI,=PL1'0'                                           
 007100          ZAP   COUNT,=PL1'0'                                            
 007200          MVC   OAMT,EDWD9                                               
 007300          ED    OAMT,PKLN                                                
 007400          MVC   OPAY,EDWD7                                               
 007500          ED    OPAY,PKPAY                                               
 007600          MVC   ORATE,EDWD5                                              
 007700          ED    ORATE,PKRATE                                             
 007800          MVC   OTERM,EDWD3                                              
 007900          ED    OTERM,PKTERM                                             
 008000          PUT   FILEOUT1,RECOUT2                                         
 008100          BR    R8                                                       
 008200 *****************************************************************       
 008300 *                   CALCULATE INTEREST ON LOAN                  *       
 008400 *****************************************************************       
 008500 CALC     EQU   *  
 008600          ZAP   MULTI,PKLN                                               
 008700          MP    MULTI,PKRATE                                             
 008800          ZAP   PKMINT,MULTI                                             
 008900          DP    PKMINT,=PL2'12'                                          
 009000          SRP   MIR,64-5,5                                               
 009100          ZAP   PRTINT,MIR                                               
 009200          ZAP   PRTPRI,PKPAY                                             
 009300          SP    PRTPRI,MIR                                               
 009400          AP    COUNT,PK1                                                
 009500          CP    COUNT,PKTERM                                             
 009600          BE    LAST                                                     
 009700          CP    PKLN,PKPAY                                               
 009800          BNH   LAST                                                     
 009900 *****************************************************************       
 010000 *        EDIT AND CALCULATE TOTALS FOR PAYMENT, INTEREST,       *       
 010100 *                      AND PRINCIPAL                            *       
 010200 *****************************************************************       
 010300 EDIT     EQU   * 
 010400          AP    TOTINT,MIR                                               
 010500          AP    TOTPRI,PRTPRI                                            
 010600          AP    TOTPAY,PKPAY                                             
 010700          SP    PKLN,PRTPRI                                              
 010800          MVC   TERMOUT,EDWD3                                            
 010900          ED    TERMOUT,COUNT                                            
 011000          MVC   PYAMT,EDWD7                                              
 011100          ED    PYAMT,PKPAY                                              
 011200          MVC   MINT,EDWD9                                               
 011300          ED    MINT,PRTINT                                              
 011400          MVC   PRINC,EDWD9                                              
 011500          ED    PRINC,PRTPRI                                             
 011600          MVC   LNBAL,EDWD9                                              
 011700          ED    LNBAL,PKLN                                               
 011800          PUT   FILEOUT1,RECOUT1                                         
 011900          B     CALC                                                     
 012000 *******************************************************************     
 012100 *                 CALCULATES THE LAST PAYMENT                     *  
 012200 *******************************************************************     
 012300 LAST     EQU   *                                                        
 012400          ZAP   MULTI,PKLN                                               
 012500          MP    MULTI,PKRATE                                             
 012600          ZAP   PKMINT,MULTI                                             
 012700          DP    PKMINT,=PL2'12'                                          
 012800          SRP   MIR,64-5,5                                               
 012900          AP    TOTINT,MIR                                               
 013000          ZAP   PRTINT,MIR                                               
 013100          AP    PKLN,MIR                                                 
 013200          AP    TOTPAY,PKLN                                              
 013300          ZAP   PRTPRI,PKLN                                              
 013400          SP    PRTPRI,MIR                                               
 013500          AP    TOTPRI,PRTPRI                                            
 013600          MVC   POUT3,EDWD9                                              
 013700          ED    POUT3,PKLN                                               
 013800          SP    PKLN,PKLN                                                
 013900          BR    R8  
 014000 ******************************************************************      
 014100 *                PRINTS THE LAST PAYMENT                         *      
 014200 ******************************************************************      
 014300 PRTLAST  EQU   *                                                        
 014400          MVC   TOUT3,EDWD3                                              
 014500          ED    TOUT3,COUNT                                              
 014600          MVC   IOUT3,EDWD9                                              
 014700          ED    IOUT3,PRTINT                                             
 014800          MVC   PROUT3,EDWD9                                             
 014900          ED    PROUT3,PRTPRI                                            
 015000          MVC   LBOUT3,EDWD9                                             
 015100          ED    LBOUT3,PKLN                                              
 015200          PUT   FILEOUT1,RECOUT3                                         
 015300          BR    R8                                                       
 015400 *****************************************************************       
 015500 *                       PRINT TOTALS                            *       
 015600 *****************************************************************       
 015700 PRTTOT   EQU   *             
 015800          MVC   PAYTOT,EDWD9                                             
 015900          ED    PAYTOT,TOTPAY                                            
 016000          MVC   MINTOT,EDWD9                                             
 016100          ED    MINTOT,TOTINT                                            
 016200          MVC   PICTOT,EDWD9                                             
 016300          ED    PICTOT,TOTPRI                                            
 016400          PUT   FILEOUT1,TOTALS                                          
 016500          BR    R8                                                       
 016600 ******************************************************************      
 016700 *    WORK AREA DATA DEFINITIONS                                         
 016800 ******************************************************************      
 016900 PK1      DC    PL1'1'                                                   
 017000 RECOUNT  DC    PL2'0'                                                   
 017100 CLEAR    DC    CL80' '                                                  
 017200 COUNT    DC    PL2'0'                                                   
 017300 PKLN     DC    PL5'0'                                                   
 017400 PKRATE   DC    PL3'0'                                                   
 017500 PKPAY    DC    PL4'0'   
 017600 PKTERM   DC    PL2'0'                                                   
 017700 MULTI    DC    PL8'0'                                                   
 017800 PKMINT   DC   0PL8'0'                                                   
 017900 MIR      DC    PL6'0'                                                   
 018000 REM      DC    PL2'0'                                                   
 018100 TOTPAY   DC    PL5'0'                                                   
 018200 TOTINT   DC    PL5'0'                                                   
 018300 TOTPRI   DC    PL5'0'                                                   
 018400 PRTINT   DC    PL5'0'                                                   
 018500 PRTPRI   DC    PL5'0'                                                   
 018600 EDWD9    DC    XL14'40206B2020206B2021204B202060'                       
 018700 EDWD7    DC    XL11'4020206B2020204B202060'                             
 018800 EDWD5    DC    XL8'4021204B20202060'                                    
 018900 EDWD3    DC    XL5'4020202060'                                          
 019000 ******************************************************************      
 019100 *     INPUT FILE - DATA CONTROL BLOCK                           *       
 019200 ******************************************************************      
 019300 FILEIN1  DCB   DSORG=PS,                                               X
 019400                MACRF=(GM),                                             X
 019500                DEVD=DA,                                                X
 019600                DDNAME=FILEIN1,                                         X
 019700                EODAD=EOF1,                                             X
 019800                RECFM=FB,                                               X
 019900                LRECL=80                                                 
 020000 ******************************************************************      
 020100 *    INPUT RECORD AREA                                                  
 020200 ******************************************************************      
 020300 RECIN1   DS   0CL80                                                     
 020400 LNAMT    DS    CL9                                                      
 020500          DS    CL1                                                      
 020600 INTRATE  DS    CL5                                                      
 020700          DS    CL5                                                      
 020800 PAYMENT  DS    CL7                                                      
 020900          DS    CL3                                                      
 021000 TERM     DS    CL3                                                      
 021100          DS    CL47     
 021200 ******************************************************************      
 021300 *     OUTPUT FILE - DATA CONTROL BLOCK                           *      
 021400 ******************************************************************      
 021500 FILEOUT1 DCB   DSORG=PS,                                               X
 021600                MACRF=(PM),                                             X
 021700                DEVD=DA,                                                X
 021800                DDNAME=FILEOUT1,                                        X
 021900                RECFM=FM,                                               X
 022000                LRECL=80                                                 
 022100 ******************************************************************      
 022200 *    OUTPUT RECORD AREAS                                                
 022300 ******************************************************************      
 022400 *      HERE IS THE HEADER FOR ** C S U **                               
 022500 ******************************************************************      
 022600 PRHEAD   DS   0CL80                                                     
 022700 PRC1     DC    CL1' '            PRINT CONTROL - SINGLE SPACE           
 022800          DC    CL15' '           SPACING OF 10 CHARACTERS               
 022900          DC    CL35'***CSU AMORTIZATION SPRING 2017***'               
 023000          DC    CL29' - OLIVIA HORACE'                                   
 023100 ******************************************************************      
 023200 *                       TOTAL HEADER                             *      
 023300 ******************************************************************      
 023400 TOTALS   DS   0CL80                                                     
 023500          DC    CL1' '                                                   
 023600          DC    CL6'TOTALS'                                              
 023700          DC    CL1' '                                                   
 023800 PAYTOT   DC    CL14' '                                                  
 023900          DC    CL7' '                                                   
 024000 MINTOT   DC    CL14' '                                                  
 024100          DC    CL1' '                                                   
 024200 PICTOT   DC    CL14' '                                                  
 024300          DS    CL22                                                     
 024400 ******************************************************************      
 024500 * HERE IS THE DETAIL OUTPUT LINE                                        
 024600 * OUTPUT FOR REGULAR PAYMENTS                                           
 024700 ******************************************************************    
 024800 RECOUT1  DS   0CL80              PRINT AREA                             
 024900 PRC2     DC    CL1' '            PRINT CONTROL CHARACTER                
 025000 TERMOUT  DC    CL5' '                                                   
 025100          DC    CL5' '                                                   
 025200 PYAMT    DC    CL11' '                                                  
 025300          DC    CL7' '                                                   
 025400 MINT     DC    CL14' '                                                  
 025500          DC    CL1' '                                                   
 025600 PRINC    DC    CL14' '                                                  
 025700          DC    CL2' '                                                   
 025800 LNBAL    DC    CL14' '                                                  
 025900          DS    CL10                                                     
 026000 *******************************************************************     
 026100 *                OUTPUT LINE FOR HEADINGS                          *    
 026200 *HEADER WITH LOAN INFORMATION                                           
 026300 *******************************************************************     
 026400 RECOUT2  DS   0CL80                                                     
 026500 PRC3     DC    CL1' '   
 026600          DC    CL7'AMOUNT:'                                             
 026700 OAMT     DC    CL14' '                                                  
 026800          DC    CL10'  PAYMENT:'                                         
 026900 OPAY     DC    CL11' '                                                  
 027000          DC    CL7'  RATE:'                                             
 027100 ORATE    DC    CL8' '                                                   
 027200          DC    CL7'  TERM:'                                             
 027300 OTERM    DC    CL5' '                                                   
 027400          DS    CL10                                                     
 027500 *******************************************************************     
 027600 *                 HEADING FOR LAST PAYMENT                        *     
 027700 *******************************************************************     
 027800 RECOUT3  DC   0CL80                                                     
 027900 PRC4     DC    CL1' '                                                   
 028000 TOUT3    DC    CL5' '                                                   
 028100          DC    CL2' '                                                   
 028200 POUT3    DC    CL14' '                                                  
 028300          DC    CL7' '     
 028400 IOUT3    DC    CL14' '                                                  
 028500          DC    CL1' '                                                   
 028600 PROUT3   DC    CL14' '                                                  
 028700          DC    CL2' '                                                   
 028800 LBOUT3   DC    CL14' '                                                  
 028900          DS    CL6                                                      
 029000 ******************************************************************      
 029100 *    REGISTER SAVE AREA                                                 
 029200 ******************************************************************      
 029300 SAVEAREA DS  18F                 ROOM FOR STORAGE OF REGISTERS          
 029400 ******************************************************************      
 029500 *     REGISTER EQUATES                                           *      
 029600 ******************************************************************      
 029700 R0       EQU   0                                                        
 029800 R1       EQU   1                                                        
 029900 R2       EQU   2                                                        
 030000 R3       EQU   3                                                        
 030100 R4       EQU   4     
 030200 R5       EQU   5                                                        
 030300 R6       EQU   6                                                        
 030400 R7       EQU   7                                                        
 030500 R8       EQU   8                                                        
 030600 R9       EQU   9                                                        
 030700 R10      EQU   10                                                       
 030800 R11      EQU   11                                                       
 030900 R12      EQU   12                                                       
 031000 R13      EQU   13                                                       
 031100 R14      EQU   14                                                       
 031200 R15      EQU   15                                                       
 031300 ******************************************************************      
 031400 *    LITERAL POOL - THIS PROGRAM MAY USE LITERALS.                      
 031500 ******************************************************************      
 031600          LTORG *                                                        
 031700          END   PROG6                                                    
 031800 /*                                                                      
 031900 //G.SYSABOUT DD SYSOUT=*     
 032000 //G.SYSUDUMP DD SYSOUT=*                                                
 032100 //G.FILEOUT1 DD SYSOUT=*,OUTLIM=2500                                    
 032200 //*G.FILEIN1  DD DSN=CSU00&ID..C3121.ASM(DATAPRG&PROG),DISP=SHR         
 032300 //G.FILEIN1  DD DSN=CSU.PUBLIC.DATA(DATAPRG&PROG),DISP=SHR              
 032400 //                                                                      
 ****** **************************** Bottom of Data ****************************
```