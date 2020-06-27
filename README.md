# utl-web-scraping-a-large-wikipedia-html-table-user-R-rvest
Scraping a large wikipedia html table user R rvest    

    Scraping a large wikipedia html table user R rvest                                                                                                          
                                                                                                                                                                
    Stackoverflow R                                                                                                                                             
    https://tinyurl.com/y47yjkzc                                                                                                                                
    https://stackoverflow.com/questions/55955700/error-in-web-scraping-in-r-from-wikipedia                                                                      
                                                                                                                                                                
    github                                                                                                                                                      
    https://tinyurl.com/ycjcrvas                                                                                                                                
    https://github.com/rogerjdeangelis/utl_R_sas_v5_xport_with_long_variable_names                                                                              
                                                                                                                                                                
    macros                                                                                                                                                      
    https://tinyurl.com/y9nfugth                                                                                                                                
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                                                  
                                                                                                                                                                
    Other web scarping repos                                                                                                                                    
    https://tinyurl.com/yd7fyp6g                                                                                                                                
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=scrape&type=&language=                                                                 
                                                                                                                                                                
                                                                                                                                                                
    I used my utl_res macro(on end) to rename the V5 transport truncated column names using                                                                     
    the labels imbeded in the transport file.                                                                                                                   
                                                                                                                                                                
    *_                   _                                                                                                                                      
    (_)_ __  _ __  _   _| |_                                                                                                                                    
    | | '_ \| '_ \| | | | __|                                                                                                                                   
    | | | | | |_) | |_| | |_                                                                                                                                    
    |_|_| |_| .__/ \__,_|\__|                                                                                                                                   
            |_|                                                                                                                                                 
    ;                                                                                                                                                           
                                                                                                                                                                
    A large HTML Table                                                                                                                                          
                                                                                                                                                                
    https://en.wikipedia.org/wiki/List_of_S%26P_500_companies                                                                                                   
                                                                                                                                                                
    This is the key html source line                                                                                                                            
                                                                                                                                                                
    <table class="wikitable sortable" id="constituents">                                                                                                        
                                                                                                                                                                
    S&P 500 Component Stocks                                                                                                                                    
                                                                                                                                                                
                                                                                                                                                                
                                                                                                                                                                
    +--------------------------------------------------------------------------------------------------------------------------------------------------------+  
    |                                                                                                                                                        |  
    |                                                                                                                                   DATE                 |  
    |                                  SEC                                                                                              FIRST                |  
    | SYMBOL     SECURITY              FILINGS     GICS SECTOR     GICS SUB INDUSTRY         HEADQUARTERS LOCATION         ADDED         CIK    FOUNDED      |  
    |                                                                                                                                                        |  
    |  MMM       3M Company            reports     Industrials     Industrial Conglomerates  St. Paul, Minnesota                         66740    1902       |  
    |  ABT       Abbott Laboratories   reports     Health Care     Health Care Equipment     North Chicago, Illinois     1964-03-31       1800    1888       |  
    |  ABBV      AbbVie Inc.           reports     Health Care     Pharmaceuticals           North Chicago, Illinois     2012-12-31    1551152    2013 (1888)|  
    |  ABMD      ABIOMED Inc           reports     Health Care     Health Care Equipment     Danvers, Massachusetts      2018-05-31     815094    1981       |  
    | ...                                                                                                                                                    |  
    +--------------------------------------------------------------------------------------------------------------------------------------------------------+  
                                                                                                                                                                
    *            _               _                                                                                                                              
      ___  _   _| |_ _ __  _   _| |_                                                                                                                            
     / _ \| | | | __| '_ \| | | | __|                                                                                                                           
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                                            
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                                           
                    |_|                                                                                                                                         
    ;                                                                                                                                                           
                                                                                                                                                                
    Note the labels in the V5 transport file were used to reame the trucated 8 char names                                                                       
                                                                                                                                                                
    Cannot use the name WANT                                                                                                                                    
    WORK.WANT_LOG_NAMES total obs=505                                                                                                                           
                                                                                                                                DATE_                           
                                    SEC_                                                                                        FIRST_                          
     SYMBOL SECURITY              FILINGS  GICS_SECTOR             GICS_SUB_INDUSTRY               HEADQUARTERS_LOCATION        ADDED     CIK      FOUNDED      
                                                                                                                                                                
     MMM    3M Company            reports  Industrials             Industrial Conglomerates        St. Paul, Minnesota                    66740    1902         
     ABT    Abbott Laboratories   reports  Health Care             Health Care Equipment           North Chicago, Illinois    1964-03-31  1800     1888         
     ABBV   AbbVie Inc.           reports  Health Care             Pharmaceuticals                 North Chicago, Illinois    2012-12-31  1551152  2013 (1888)  
     ABMD   ABIOMED Inc           reports  Health Care             Health Care Equipment           Danvers, Massachusetts     2018-05-31  815094   1981         
     ACN    Accenture plc         reports  Information Technology  IT Consulting & Other Services  Dublin, Ireland            2011-07-06  1467373  1989         
     ATVI   Activision Blizzard   reports  Communication Services  Interactive Home Entertainment  Santa Monica, California   2015-08-31  718877   2008         
    ..                                                                                                                                                          
                                                                                                                                                                
    *                                                                                                                                                           
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                                          
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                                                         
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                                         
    | .__/|_|  \___/ \___\___||___/___/                                                                                                                         
    |_|                                                                                                                                                         
    ;                                                                                                                                                           
                                                                                                                                                                
    %utl_submit_r64('                                                                                                                                           
    library(rvest);                                                                                                                                             
    library(SASxport);                                                                                                                                          
    library(data.table);                                                                                                                                        
    want <- read_html("https://en.wikipedia.org/wiki/List_of_S%26P_500_companies") %>%                                                                          
      html_nodes("#constituents") %>%                                                                                                                           
      html_table();                                                                                                                                             
    want<-as.data.frame(want);                                                                                                                                  
    lbl<-colnames(want);                                                                                                                                        
    for(i in seq_along(want)){                                                                                                                                  
      label(want[, i]) <- lbl[i];                                                                                                                               
    };                                                                                                                                                          
    label(want);                                                                                                                                                
    write.xport(want, file="d:/xpt/want.xpt");                                                                                                                  
    ');                                                                                                                                                         
                                                                                                                                                                
    * just in case;                                                                                                                                             
    %symdel want / nowarn;                                                                                                                                      
    proc datasets lib=work;                                                                                                                                     
    delete want                                                                                                                                                 
    run;quit;                                                                                                                                                   
                                                                                                                                                                
    libname xpt xport "d:/xpt/want.xpt";                                                                                                                        
                                                                                                                                                                
                                                                                                                                                                
    /* Note truncated name with lon variable names in the sas label                                                                                             
                                                                                                                                                                
    proc contents data=xpt.want;                                                                                                                                
    run;quit;                                                                                                                                                   
                                                                                                                                                                
                                                                                                                                                                
         Alphabetic List of Variables and Attributes                                                                                                            
                                                                                                                                                                
    #    Variable    Type    Len    Label                                                                                                                       
                                                                                                                                                                
     1    SYMBOL      Char      5    Symbol                                                                                                                     
     2    SECURITY    Char     38    Security                                                                                                                   
     3    SEC_FILI    Char      7    SEC.filings                                                                                                                
     4    GICS_SEC    Char     22    GICS.Sector                                                                                                                
     5    GICS_SUB    Char     44    GICS.Sub.Industry                                                                                                          
     6    HEADQUAR    Char     36    Headquarters.Location                                                                                                      
     7    DATE_FIR    Char     10    Date.first.added                                                                                                           
     8    CIK         Char      7    CIK                                                                                                                        
     9    FOUNDED     Char     16    Founded                                                                                                                    
    */                                                                                                                                                          
                                                                                                                                                                
    proc datasets lib=work mt=view mt=data;                                                                                                                                                                                                                         
       delete __ren001 want;                                                                                                                                                                                                                                          
    run;quit;                                                                                                                                                                                                                                                       
                                                                                                                                                                                                                                                                
    /* need this if you rerun                                                                                                                                                                                                                                       
    NOTE: Deleting WORK.__REN001 (memtype=DATA).                                                                                                                                                                                                                    
    NOTE: Deleting WORK.WANT (memtype=VIEW).                                                                                                                                                                                                                        
    */            
                                                                                                                                                            
    data want_log_names; *===> cannot use name want;                                                                                                            
                                                                                                                                                                
      %utl_rens(xpt.want);                                                                                                                                      
      set want;                                                                                                                                                 
                                                                                                                                                                
    run;quit;                                                                                                                                                   
                                                                                                                                                                
    /* now have long variable names                                                                                                                             
                                                                                                                                                                
                        Variables in Creation Order                                                                                                             
                                                                                                                                                                
     #    Variable                 Type    Len    Label                                                                                                         
                                                                                                                                                                
     1    SYMBOL                   Char      5    Symbol                                                                                                        
     2    SECURITY                 Char     38    Security                                                                                                      
     3    SEC_FILINGS              Char      7    SEC.filings                                                                                                   
     4    GICS_SECTOR              Char     22    GICS.Sector                                                                                                   
     5    GICS_SUB_INDUSTRY        Char     44    GICS.Sub.Industry                                                                                             
     6    HEADQUARTERS_LOCATION    Char     36    Headquarters.Location                                                                                         
     7    DATE_FIRST_ADDED         Char     10    Date.first.added                                                                                              
     8    CIK                      Char      7    CIK                                                                                                           
     9    FOUNDED                  Char     16    Founded                                                                                                       
    */                                                                                                                                                          
                                                                                                                                                                
                                                                                                                                                                
    *                                                                                                                                                           
     _ __ ___   __ _  ___ _ __ ___                                                                                                                              
    | '_ ` _ \ / _` |/ __| '__/ _ \                                                                                                                             
    | | | | | | (_| | (__| | | (_) |                                                                                                                            
    |_| |_| |_|\__,_|\___|_|  \___/                                                                                                                             
                                                                                                                                                                
    ;                                                                                                                                                           
                                                                                                                                                                
    %macro utl_rens(dsn)/des="use with R SASXport for long variable names";                                                                                     
                                                                                                                                                                
      if _n_=0 then do;                                                                                                                                         
                                                                                                                                                                
        rc=%sysfunc(dosubl('                                                                                                                                    
            data __ren001;                                                                                                                                      
               set &dsn(obs=1);                                                                                                                                 
            run;quit;                                                                                                                                           
            proc transpose data=__ren001 out=__ren002(drop=col1);                                                                                               
              var _all_;                                                                                                                                        
            run;quit;                                                                                                                                           
            proc sql;                                                                                                                                           
              select                                                                                                                                            
                catx(" ",_name_,"as",translate(lbl,"_",".")) into :rens separated by ","                                                                        
              from                                                                                                                                              
                (                                                                                                                                               
                 select                                                                                                                                         
                    _name_                                                                                                                                      
                   ,case                                                                                                                                        
                        when (_label_ = " ") then _name_                                                                                                        
                        else _label_                                                                                                                            
                    end as lbl                                                                                                                                  
                 from                                                                                                                                           
                    __ren002                                                                                                                                    
                )                                                                                                                                               
           ;quit;                                                                                                                                               
            proc sql;                                                                                                                                           
               create                                                                                                                                           
                   view %scan(&dsn,2,".")  as                                                                                                                   
               select                                                                                                                                           
                   &rens                                                                                                                                        
               from                                                                                                                                             
                   &dsn.                                                                                                                                        
            ;quit;                                                                                                                                              
        '));                                                                                                                                                    
        drop rc;                                                                                                                                                
      end;                                                                                                                                                      
                                                                                                                                                                
    %mend utl_rens;                                                                                                                                             
                                                                                                                                                                
