# utl-select-classes-attended-by-Jane-john-and-judy-using-sas-r-and-python-sql-muti-language
Select classes attended by jane john and judy using sas r and python sql muti language
    %let pgm=utl-select-classes-attended-by-Jane-john-and-judy-using-sas-r-and-python-sql-muti-language;

    %stop_submission;

    Select classes attended by jane john and judy using sas r and python sql muti language

         SOLUTIONS

             1 sas sql
             2 r sql (note sqlite does not return all records in a group using having.
               It only returns the class that satisfies the having clause? You need a subquery
             3 python sql (same code as in r, FYI in memory SQLLITE has different syntax from r in memory sqllite?

    github
    https://tinyurl.com/43p58hxr
    https://github.com/rogerjdeangelis/utl-select-classes-attended-by-Jane-john-and-judy-using-sas-r-and-python-sql-muti-language

    Related repos
    ttps://tinyurl.com/24xj52bs
    https://github.com/rogerjdeangelis/utl-using-a-bolean-truth-table-for-complex-filtering-in-sql-sas-r-and-pythom-multi-language

    https://tinyurl.com/4ha67e8z
    https://github.com/rogerjdeangelis/utl-count-grocery-items-and-fraction-dairy-by-customer-using-r-dplyr-language-and-sql-sas-r-python

    stackoverflow SAS
    https://tinyurl.com/5d692pjd
    https://communities.sas.com/t5/SAS-Programming/How-to-group-userid-cardid-with-multiple-transaction-codes/m-p/949770#M371493


    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                               |                                  |                                     */
    /*           INPUT                               |        PROCESS                   |        OUTPUT                       */
    /*  DATA DOES HAVE TO BE SORTED                  |      SELF EXPLANATORY            |   MATH IS MISSING(NO John)          */
    /*                                               |                                  |                                     */
    /*                                               |  SAS                             |                                     */
    /*                                               |  ===                             |                                     */
    /*                                               |   select                                                     |                                     */
    /*  CLASS    NAME       SEX                      |     *                            |  NAME       SEX    CLASS            */
    /*                                               |   from                           |                                     */
    /*  CIVICS   James       M HAS ALL THREE         |     sd1.have                     |  Judy        F     CIVICS           */
    /*  CIVICS   Jane        F                       |   group                          |  Jeffrey     M     CIVICS           */
    /*  CIVICS   Janet       F                       |     by class                     |  James       M     CIVICS           */
    /*  CIVICS   Jeffrey     M                       |   having                         |  Janet       F     CIVICS           */
    /*  CIVICS   John        M                       |   /*--- =1 is not needed ---*/   |  John        M     CIVICS           */
    /*  CIVICS   Joyce       F                       |          max(name="Jane") = 1    |  Joyce       F     CIVICS           */
    /*  CIVICS   Judy        F                       |     and  max(name="John") = 1    |  Jane        F     CIVICS           */
    /*                                               |     and  max(name="Judy") = 1    |                           No MATH   */
    /*  MATH     James       M DO NOT OUPUT MATH     |   order                          |  John        M     MUSIC            */
    /*  MATH     Jane        F BECAUSE John DID      |     by class, name               |  James       M     MUSIC            */
    /*  MATH     Janet       F NOT ATTEND THIS CLASS |                                  |  Jane        F     MUSIC            */
    /*  MATH     Jeffrey     M                       |----------------------------------|  Jeffrey     M     MUSIC            */
    /*  MATH     Joyce       F                       |                                  |  Judy        F     MUSIC            */
    /*  MATH     Judy        F                       |  R AND PYTHON                    |  Janet       F     MUSIC            */
    /*                                               |  =============                   |  Joyce       F     MUSIC            */
    /*  MUSIC    James       M HAS ALL THREE         |                                  |                                     */
    /*  MUSIC    Jane        F                       |     select                       |                                     */
    /*  MUSIC    Janet       F                       |      *                           |                                     */
    /*  MUSIC    Jeffrey     M                       |     from                         |                                     */
    /*  MUSIC    John        M                       |      have                        |                                     */
    /*  MUSIC    Joyce       F                       |     where                        |                                     */
    /*  MUSIC    Judy        F                       |      class in (                  |                                     */
    /*                                               |        select                    |                                     */
    /*  AUTUAL DATA                                  |           class                  |                                     */
    /*                                               |        from                      |                                     */
    /*  NAME       SEX    CLASS                      |           have                   |                                     */
    /*                                               |        group                     |                                     */
    /*  James       M     CIVICS                     |          by class                |                                     */
    /*  James       M     MATH                       |        having                    |                                     */
    /*  James       M     MUSIC                      |               max(name="Jane")   |                                     */
    /*  Jane        F     CIVICS                     |          and  max(name="John")   |                                     */
    /*  Jane        F     MATH                       |          and  max(name="Judy")   |                                     */
    /*  Jane        F     MUSIC                      |        )                         |                                     */
    /*  Janet       F     CIVICS                     |     rder                         |                                     */
    /*  Janet       F     MATH                       |       by class, name             |                                     */
    /*  Janet       F     MUSIC                      |                                  |                                     */
    /*  Jeffrey     M     CIVICS                     |                                  |                                     */
    /*  Jeffrey     M     MATH                       |                                  |                                     */
    /*  Jeffrey     M     MUSIC                      |                                  |                                     */
    /*  John        M     CIVICS                     |                                  |                                     */
    /*  John        M     MUSIC                      |                                  |                                     */
    /*  Joyce       F     CIVICS                     |                                  |                                     */
    /*  Joyce       F     MATH                       |                                  |                                     */
    /*  Joyce       F     MUSIC                      |                                  |                                     */
    /*  Judy        F     CIVICS                     |                                  |                                     */
    /*  Judy        F     MATH                       |                                  |                                     */
    /*  Judy        F     MUSIC                      |                                  |                                     */
    /*                                               |                                  |                                     */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      set sashelp.class(keep=name sex where=(name =: "J"));
      do class = "CIVICS","MATH","MUSIC";
       if (class="MATH" and name eq "John") then continue;
       else output;
    end;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  NAME       SEX    CLASS                                                                                               */
    /*                                                                                                                        */
    /*  James       M     CIVICS                                                                                              */
    /*  James       M     MATH                                                                                                */
    /*  James       M     MUSIC                                                                                               */
    /*  Jane        F     CIVICS                                                                                              */
    /*  Jane        F     MATH                                                                                                */
    /*  Jane        F     MUSIC                                                                                               */
    /*  Janet       F     CIVICS                                                                                              */
    /*  Janet       F     MATH                                                                                                */
    /*  Janet       F     MUSIC                                                                                               */
    /*  Jeffrey     M     CIVICS                                                                                              */
    /*  Jeffrey     M     MATH                                                                                                */
    /*  Jeffrey     M     MUSIC                                                                                               */
    /*  John        M     CIVICS                                                                                              */
    /*  John        M     MUSIC                                                                                               */
    /*  Joyce       F     CIVICS                                                                                              */
    /*  Joyce       F     MATH                                                                                                */
    /*  Joyce       F     MUSIC                                                                                               */
    /*  Judy        F     CIVICS                                                                                              */
    /*  Judy        F     MATH                                                                                                */
    /*  Judy        F     MUSIC                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc sql;
      create
        table want as
      select
        *
      from
        sd1.have
      group
        by class
      having
      /*--- =1 is not needed ---*/
             max(name="Jane")
        and  max(name="John")
        and  max(name="Judy")
      order
        by class, name
    ;quit;

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    print(have)
    str(have)
    want <- sqldf('
       select
        *
       from
        have
       where
        class in (
          select
             class
          from
             have
          group
            by class
          having
                 max(name="Jane")
            and  max(name="John")
            and  max(name="Judy")
          )
      order
         by class, name
      ')
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                           |                                                                                            */
    /*  R                        |  SAS                                                                                       */
    /*                           |                                                                                            */
    /*        NAME SEX  CLASS    |  ROWNAMES    NAME       SEX    CLASS                                                       */
    /*                           |                                                                                            */
    /*  1    James   M CIVICS    |      1       James       M     CIVICS                                                      */
    /*  2     Jane   F CIVICS    |      2       Jane        F     CIVICS                                                      */
    /*  3    Janet   F CIVICS    |      3       Janet       F     CIVICS                                                      */
    /*  4  Jeffrey   M CIVICS    |      4       Jeffrey     M     CIVICS                                                      */
    /*  5     John   M CIVICS    |      5       John        M     CIVICS                                                      */
    /*  6    Joyce   F CIVICS    |      6       Joyce       F     CIVICS                                                      */
    /*  7     Judy   F CIVICS    |      7       Judy        F     CIVICS                                                      */
    /*  8    James   M  MUSIC    |      8       James       M     MUSIC                                                       */
    /*  9     Jane   F  MUSIC    |      9       Jane        F     MUSIC                                                       */
    /*  10   Janet   F  MUSIC    |     10       Janet       F     MUSIC                                                       */
    /*  11 Jeffrey   M  MUSIC    |     11       Jeffrey     M     MUSIC                                                       */
    /*  12    John   M  MUSIC    |     12       John        M     MUSIC                                                       */
    /*  13   Joyce   F  MUSIC    |     13       Joyce       F     MUSIC                                                       */
    /*  14    Judy   F  MUSIC    |     14       Judy        F     MUSIC                                                       */
    /*                           |                                                                                            */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */
    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
       select
        *
       from
        have
       where
        class in (
          select
             class
          from
             have
          group
            by class
          having
                 max(name="Jane")
            and  max(name="John")
            and  max(name="Judy")
          )
      order
         by class, name
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*                            |                                                                                           */
    /* MATH MISSING               |                                                                                           */
    /*                            | SAS                                                                                       */
    /* PYTHON                     |                                                                                           */
    /*         NAME SEX   CLASS   |  NAME       SEX    CLASS                                                                  */
    /*                            |                                                                                           */
    /*  0     James   M  CIVICS   |  James       M     CIVICS                                                                 */
    /*  1      Jane   F  CIVICS   |  Jane        F     CIVICS                                                                 */
    /*  2     Janet   F  CIVICS   |  Janet       F     CIVICS                                                                 */
    /*  3   Jeffrey   M  CIVICS   |  Jeffrey     M     CIVICS                                                                 */
    /*  4      John   M  CIVICS   |  John        M     CIVICS                                                                 */
    /*  5     Joyce   F  CIVICS   |  Joyce       F     CIVICS                                                                 */
    /*  6      Judy   F  CIVICS   |  Judy        F     CIVICS                                                                 */
    /*  7     James   M   MUSIC   |  James       M     MUSIC                                                                  */
    /*  8      Jane   F   MUSIC   |  Jane        F     MUSIC                                                                  */
    /*  9     Janet   F   MUSIC   |  Janet       F     MUSIC                                                                  */
    /*  10  Jeffrey   M   MUSIC   |  Jeffrey     M     MUSIC                                                                  */
    /*  11     John   M   MUSIC   |  John        M     MUSIC                                                                  */
    /*  12    Joyce   F   MUSIC   |  Joyce       F     MUSIC                                                                  */
    /*  13     Judy   F   MUSIC   |  Judy        F     MUSIC                                                                  */
    /*                            |                                                                                           */
    /***************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

