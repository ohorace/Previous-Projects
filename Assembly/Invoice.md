```Assembly   
File  Edit  Edit_Settings  Menu  Utilities  Compilers  Test  Help            
 sssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss
 EDIT       CSU0014.C3121.ASM(PROG5) - 01.99                Columns 00001 00072 
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
 000700 //        SET   PROG=5                                                  
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
 002100 PROG5    CSECT                                                          
 002200          STM   R14,R12,12(R13)         STORE EXISTING REGISTERS         
 002300          LR    R12,R15                 ESTABLISH 1ST BASE REG           
 002400          USING PROG5,R12,R11,R10       DEFINING THREE BASE REGS         
 002500          LAY   R11,PROG5+4096          SECOND BASE REG + 4K             
 002600          LAY   R10,PROG5+8192          THIRD BASE REG + 8K              
 002700          ST    R13,SAVEAREA+4          BACKWARD CHAIN CALLER'S          
 002800          LA    R13,SAVEAREA            ADDRESS OF MY SAVE AREA          
 002900 ******************************************************************      
 003000 * BEGIN THE PROGRAM LOGIC. FIRST OPEN THE INPUT AND OUTPUT FILES *      
 003100 ****************************************************************** 
 003200          OPEN  (FILEIN1,(INPUT))      OPEN INPUT FILE                   
 003300          OPEN  (FILEOUT1,(OUTPUT))    OPEN OUTPUT FILE                  
 003400          PUT   FILEOUT1,PRHEAD         OUTPUT THE HEADER                
 003500          PUT   FILEOUT1,RPHEAD                                          
 003600          PUT   FILEOUT1,LABLHD                                          
 003700          GET   FILEIN1,RECIN1          GET THE FIRST RECORD, IF ONE     
 003800 ******************************************************************      
 003900 *        READ AND PRINT LOOP                                     *      
 004000 ******************************************************************      
 004100 LOOP     EQU   *                                                        
 004200          AP    RECOUNT,PK1             INCREMENT RECORD COUNT           
 004300          BAS   R8,CALCC                                                 
 004400          BAS   R8,EDIT                                                  
 004500          GET   FILEIN1,RECIN1                                           
 004600          B     LOOP                    GO BACK AND PROCESS              
 004700 ******************************************************************      
 004800 *        END OF INPUT PROCESSING                                 *      
 004900 ****************************************************************** 
 005000 EOF1     EQU   *                                                        
 005100          BAS   R8,PRTT                                                  
 005200          BAS   R8,CALAVG                                                
 005300          BAS   R8,PRTA                                                  
 005400          CLOSE (FILEIN1)               CLOSE INPUT FILE                 
 005500          CLOSE (FILEOUT1)              CLOSE OUTPUT FILE                
 005600          L     R13,SAVEAREA+4          POINT AT OLD SAVE AREA           
 005700          LM    R14,R12,12(R13)         RESTORE THE REGISTERS            
 005800          LA    R15,0                   RETURN CODE = 0                  
 005900          BR    R14                                                      
 006000 ******************************************************************      
 006100 *      PACK NUMBERS AND UPDATE TOTAL COST AND TOTAL QUANTITY     *      
 006200 ******************************************************************      
 006300 CALCC    EQU   *                                                        
 006400          PACK  PACKQ,QUAN                                               
 006500          PACK  PACKP,PRICE                                              
 006600          ZAP   PACKC,PACKQ                                              
 006700          AP    TOTQUA,PACKQ 
 006800          MP    PACKC,PACKP                                              
 006900          AP    TOTCOS,PACKC                                             
 007000          BR    R8                                                       
 007100 ********************************************************************    
 007200 *     PRINT QUANTITY, PRICE, AND COST - SHIFT QUANTITY LEFT TWO    *    
 007300 ********************************************************************    
 007400 EDIT     EQU   *                                                        
 007500          MVC   ONAME,NAME                                               
 007600          SRP   PACKQ,2,0                                                
 007700          MVC   OQUAN,EDWD13                                             
 007800          ED    OQUAN,PACKQ                                              
 007900          MVC   OPRICE,EDWD8                                             
 008000          ED    OPRICE,PACKP                                             
 008100          MVC   OCOST,EDWD16                                             
 008200          ED    OCOST,PACKC                                              
 008300          PUT   FILEOUT1,RECOUT1                                         
 008400          BR    R8                                                       
 008500 *******************************************************************
 008600 *   CALCULATE TOTALS FOR QUANTITY AND COSTS. SHIFTS ONE TO THE    *     
 008700 *   LEFT BEFORE DIVIDING, THEN SHIFT ONE TO THE RIGHT WHEN DONE  *      
 008800 *   PRINT ROUTINE CALLED BEFORE THIS SHIFTS TOTAL PACKED FIELDS   *     
 008900 *   BY TWO, SO THEY ARE SHIFTED ONE FOR 3 DECIMAL PLACES          *     
 009000 *   THEN ONE IS ROUNDED OFF                                       *     
 009100 *******************************************************************     
 009200 CALAVG   EQU   *                                                        
 009300          ZAP   WORK,TOTQUA                                              
 009400          SRP   WORK,1,0                                                 
 009500          DP    WORK,RECOUNT                                             
 009600          SRP   RES,64-1,5                                               
 009700          ZAP   AVGQUA,RES                                               
 009800          ZAP   WORK,=PL1'0'                                             
 009900          ZAP   WORK,TOTCOS                                              
 010000          SRP   WORK,1,0                                                 
 010100          DP    WORK,RECOUNT                                             
 010200          SRP   RES,64-1,5                                               
 010300          ZAP   AVGCOS,RES    
 010400          BR    R8                                                       
 010500 ********************************************************************    
 010600 *                         PRINT TOTALS                             *    
 010700 ********************************************************************    
 010800 PRTT     EQU   *                                                        
 010900          MVC   RECOUT1,CLEAR                                            
 011000          MVC   ONAME,=CL20'   TOTALS'                                   
 011100          SRP   TOTQUA,2,0                                               
 011200          MVC   OQUAN,EDWD13                                             
 011300          ED    OQUAN,TOTQUA                                             
 011400          MVC   OCOST,EDWD16                                             
 011500          ED    OCOST,TOTCOS                                             
 011600          PUT   FILEOUT1,RECOUT1                                         
 011700          BR    R8                                                       
 011800 ********************************************************************    
 011900 *                         PRINT AVERAGES                           *    
 012000 ********************************************************************    
 012100 PRTA     EQU   *   
 012200          MVC   RECOUT1,CLEAR                                            
 012300          MVC   ONAME,=CL20'   AVERAGES'                                 
 012400          MVC   OQUAN,EDWD13                                             
 012500          ED    OQUAN,AVGQUA                                             
 012600          MVC   OCOST,EDWD16                                             
 012700          ED    OCOST,AVGCOS                                             
 012800          PUT   FILEOUT1,RECOUT1                                         
 012900          BR    R8                                                       
 013000 ******************************************************************      
 013100 *    WORK AREA DATA DEFINITIONS                                         
 013200 ******************************************************************      
 013300 PK1      DC    PL1'1'            'CONSTANT' OF 1 FOR INCREMENT          
 013400 RECOUNT  DC    PL2'0'                                                   
 013500 CLEAR    DC    CL80' '                                                  
 013600 PACKP    DC    PL3'0'                                                   
 013700 PACKQ    DC    PL5'0'                                                   
 013800 PACKC    DC    PL6'0'                                                   
 013900 TOTCOS   DC    PL6'0'          
 014000 AVGCOS   DC    PL6'0'                                                   
 014100 TOTQUA   DC    PL5'0'                                                   
 014200 AVGQUA   DC    PL5'0'                                                   
 014300 WORK     DC   0PL8'0'                                                   
 014400 RES      DC    PL6'0'                                                   
 014500 REM      DC    PL2'0'                                                   
 014600 EDWD16   DC    XL16'402020206B2020206B2021204B202060'                   
 014700 EDWD13   DC    XL13'40202020206B2020204B202060'                         
 014800 EDWD8    DC    XL8'402021204B202060'                                    
 014900 ******************************************************************      
 015000 *     INPUT FILE - DATA CONTROL BLOCK                           *       
 015100 ******************************************************************      
 015200 FILEIN1  DCB   DSORG=PS,                                               X
 015300                MACRF=(GM),                                             X
 015400                DEVD=DA,                                                X
 015500                DDNAME=FILEIN1,                                         X
 015600                EODAD=EOF1,                                             X
 015700                RECFM=FB,    
 015800                LRECL=80                                                 
 015900 ******************************************************************      
 016000 *    INPUT RECORD AREA                                                  
 016100 ******************************************************************      
 016200 RECIN1   DS   0CL80                                                     
 016300          DS    CL10                                                     
 016400 NAME     DS    CL20                                                     
 016500 PRICE    DS    CL05                                                     
 016600          DS    CL05                                                     
 016700 QUAN     DS    CL05                                                     
 016800          DS    CL35                                                     
 016900 ******************************************************************      
 017000 *     OUTPUT FILE - DATA CONTROL BLOCK                           *      
 017100 ******************************************************************      
 017200 FILEOUT1 DCB   DSORG=PS,                                               X
 017300                MACRF=(PM),                                             X
 017400                DEVD=DA,                                                X
 017500                DDNAME=FILEOUT1,     
 017600                RECFM=FM,                                               X
 017700                LRECL=80                                                 
 017800 ******************************************************************      
 017900 *    OUTPUT RECORD AREAS                                                
 018000 ******************************************************************      
 018100 *      HERE IS THE HEADER FOR ** C S U **                               
 018200 ******************************************************************      
 018300 PRHEAD   DS   0CL80                                                     
 018400 PRC1     DC    CL1' '            PRINT CONTROL - SINGLE SPACE           
 018500          DC    CL30' '           SPACING OF 10 CHARACTERS               
 018600          DC    CL49'***CSU SPRING 2017***'                              
 018700 RPHEAD   DS   0CL80                                                     
 018800          DC    CL20' '                                                  
 018900          DC    CL21'SALES REPORT SUMMARY'                               
 019000          DC    CL5' '                                                   
 019100          DC    CL34'(14) -- OLIVIA HORACE'                              
 019200 LABLHD   DS   0CL80                                                     
 019300          DC    CL1' '   
 019400          DC    CL24'NAME'                                               
 019500          DC    CL16'QUANTITY'                                           
 019600          DC    CL22'PRICE'                                              
 019700          DC    CL4'COST'                                                
 019800          DS    CL13                                                     
 019900 ******************************************************************      
 020000 * HERE IS THE DETAIL OUTPUT LINE                                        
 020100 ******************************************************************      
 020200 RECOUT1  DS   0CL80              PRINT AREA                             
 020300 PRC2     DC    CL1' '            PRINT CONTROL CHARACTER                
 020400 ONAME    DC    CL20' '                                                  
 020500 OQUAN    DC    CL13' '                                                  
 020600          DC    CL5' '                                                   
 020700 OPRICE   DC    CL8' '                                                   
 020800          DC    CL5' '                                                   
 020900 OCOST    DC    CL16' '                                                  
 021000          DS    CL12                                                     
 021100 ****************************************************************** 
 021200 *    REGISTER SAVE AREA                                                 
 021300 ******************************************************************      
 021400 SAVEAREA DS  18F                 ROOM FOR STORAGE OF REGISTERS          
 021500 ******************************************************************      
 021600 *     REGISTER EQUATES                                           *      
 021700 ******************************************************************      
 021800 R0       EQU   0                                                        
 021900 R1       EQU   1                                                        
 022000 R2       EQU   2                                                        
 022100 R3       EQU   3                                                        
 022200 R4       EQU   4                                                        
 022300 R5       EQU   5                                                        
 022400 R6       EQU   6                                                        
 022500 R7       EQU   7                                                        
 022600 R8       EQU   8                                                        
 022700 R9       EQU   9                                                        
 022800 R10      EQU   10                                                       
 022900 R11      EQU   11   
 023000 R12      EQU   12                                                       
 023100 R13      EQU   13                                                       
 023200 R14      EQU   14                                                       
 023300 R15      EQU   15                                                       
 023400 ******************************************************************      
 023500 *    LITERAL POOL - THIS PROGRAM MAY USE LITERALS.                      
 023600 ******************************************************************      
 023700          LTORG *                                                        
 023800          END   PROG5                                                    
 023900 /*                                                                      
 024000 //G.SYSABOUT DD SYSOUT=*                                                
 024100 //G.SYSUDUMP DD SYSOUT=*                                                
 024200 //G.FILEOUT1 DD SYSOUT=*,OUTLIM=2500                                    
 024300 //*G.FILEIN1  DD DSN=CSU00&ID..C3121.ASM(DATAPRG&PROG),DISP=SHR         
 024400 //G.FILEIN1  DD DSN=CSU.PUBLIC.DATA(DATAPRG&PROG),DISP=SHR              
 024500 //                                                                      
 ****** **************************** Bottom of Data ****************************
 ```