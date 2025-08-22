# utl-avoid-klingon-macro-code-when-constructing-a-maco-variable-enclosed-in-percent-signs
Avoid klingon macro code when constructing a maco variable enclosed in percent signs
    %let pgm=utl-avoid-klingon-macro-code-when-constructing-a-maco-variable-enclosed-in-percent-signs;

    %stop_submission;

    Avoid klingon macro code when constructing a maco variable enclosed in percent signs

    communities.sas
    https://tinyurl.com/muz54cue
    https://communities.sas.com/t5/SAS-Programming/adding-percent-chars-to-macrovariable/m-p/761408#M240939

    github
    https://tinyurl.com/bdevsy37
    https://github.com/rogerjdeangelis/utl-avoid-klingon-macro-code-when-constructing-a-maco-variable-enclosed-in-percent-signs

    PROBLEM GIVEN

      %let strng=av;

      resolve %&strng% to "%av%"

      Note

      %put xxx "%&strng%" xxx;
      results in

      /*-- FAILS &strng not resolved --*/
      xxx "%&strng%" xxx


    /*****************************************************************************************/
    /* INPUT                     | PROCESS                              | OUTPUT             */
    /* =====                     | =======                              | ======             */
    /* TEAM      POINTS          | Select teams with av inteam name     | TEAM        POINTS */
    /*                           |                                      | ------------------ */
    /* Cavs        12            | Self explanatory has warnings        | Cavs            12 */
    /* Cavs        14            |                                      | Cavs            14 */
    /* Warriors    15            | %let strng=av;                       | Mavs            31 */
    /* Hawks       18            |                                      | Mavs            32 */
    /* Mavs        31            | data _null_;                         | Mavs            35 */
    /* Mavs        32            |   res=quote(resolve('%&strng%'));    |                    */
    /* Mavs        35            |   call symputx('lyk',res);           |                    */
    /* Celtics     36            | run;quit;                            |                    */
    /* Celtics     40            |                                      |                    */
    /*                           | proc sql;                            |                    */
    /* data my_data;             |     select *                         |                    */
    /*   input team $ points;    |     from my_data                     |                    */
    /* cards4;                   |     where team like &lyk             |                    */
    /* Cavs 12                   | ;quit;                               |                    */
    /* Cavs 14                   |                                      |                    */
    /* Warriors 15               | WARNING: Apparent invocation of      |                    */
    /* Hawks 18                  |          macro AV not resolved.      |                    */
    /* Mavs 31                   |                                      |                    */
    /* Mavs 32                   | %put --- &lyk ---;                   |                    */
    /* Mavs 35                   |                                      |                    */
    /* Celtics 36                | --- "%av%" ---                       |                    */
    /* Celtics 40                |                                      |                    */
    /* ;;;;                      |                                      |                    */
    /* run;quit;                 |                                      |                    */
    /*                           |                                      |                    */
    /*****************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
