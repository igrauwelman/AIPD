AIPD - Diagnostics and Imaging Results
================

-   [libraries](#libraries)
-   [preprocessing](#preprocessing)
-   [article specialization](#article-specialization)
    -   [article specialization total](#article-specialization-total)
    -   [percentage of experts](#percentage-of-experts)
-   [article type total](#article-type-total)
-   [sentiment](#sentiment)
    -   [sentiment total](#sentiment-total)
    -   [article specialization and percentage of
        sentiment](#article-specialization-and-percentage-of-sentiment)
    -   [author expertise and percentage of
        sentiment](#author-expertise-and-percentage-of-sentiment)
    -   [year and percentage of
        sentiment](#year-and-percentage-of-sentiment)
    -   [personal impression and percentage of
        sentiment](#personal-impression-and-percentage-of-sentiment)
-   [personal impression](#personal-impression)
    -   [personal impression total](#personal-impression-total)
    -   [article specialization and percentage of personal
        impression](#article-specialization-and-percentage-of-personal-impression)
    -   [author expertise and percentage of personal
        impression](#author-expertise-and-percentage-of-personal-impression)
    -   [year and percentage of personal
        impression](#year-and-percentage-of-personal-impression)
-   [SWOT](#swot)
    -   [SWOT total](#swot-total)
    -   [article specialization and percentage of
        SWOT](#article-specialization-and-percentage-of-swot)
    -   [author expertise and percentage of
        SWOT](#author-expertise-and-percentage-of-swot)
    -   [year and percentage of SWOT](#year-and-percentage-of-swot)
-   [synonyms](#synonyms)
    -   [synonyms total](#synonyms-total)
    -   [article specialization and percentage of
        synonyms](#article-specialization-and-percentage-of-synonyms)
    -   [author expertise and percentage of
        synonyms](#author-expertise-and-percentage-of-synonyms)
    -   [year and count of synonyms](#year-and-count-of-synonyms)
    -   [personal impression and percentage of
        synonyms](#personal-impression-and-percentage-of-synonyms)
-   [illnesses](#illnesses)
    -   [illnesses total](#illnesses-total)
    -   [year and percentage of
        illnesses](#year-and-percentage-of-illnesses)
    -   [sentiment and illnesses](#sentiment-and-illnesses)
    -   [personal impression and
        illnesses](#personal-impression-and-illnesses)
    -   [SWOT and illnesses](#swot-and-illnesses)

# libraries

``` r
library(tidyverse)
library(dplyr)
library(ggplot2)
```

# preprocessing

``` r
# load data from CATMA
CATMA <- read.csv(file = "CATMA_results_final.csv", sep = ";")
head(CATMA)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Group"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["FAZ...Sind.Algorithmen.die.besseren.Ã.rzte..D_28763721.637D.444B.ADB8.FF278C9DB23F."],"name":[3],"type":["int"],"align":["right"]},{"label":["FAZ...Sind.Algorithmen.die.besseren.Ã.rzte.Default.Annotations..C_2DAAB5CA.1118.4703.AE3E.77F03CBA5077."],"name":[4],"type":["int"],"align":["right"]},{"label":["Im.Kampf.gegen.Krebs.sind.wir.mitten.in.einer.explosiven.Entwicklung..D_2DE464EE.FF9F.4C8A.A6E6.8763FB6B98F8."],"name":[5],"type":["int"],"align":["right"]},{"label":["Im.Kampf.gegen.Krebs.sind.wir.mitten.in.einer.explosiven.Entwicklung.Default.Annotations..C_3283F2FD.8065.4F41.B2CE.7051F928F5DE."],"name":[6],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk.Kultur...KI.in.der.Medizin..D_2E5B6E46.7AC2.4F96.83C3.6DC4D8F0F7AE."],"name":[7],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk.Kultur...KI.in.der.Medizin.Default.Annotations..C_D3153C5D.A3ED.4E3A.A96D.07FAEEB7F654."],"name":[8],"type":["int"],"align":["right"]},{"label":["Ã.rzteblatt...KÃ.nstliche.Intelligenz.soll.MRT.Auswertung.beschleunigen..D_3878BC46.DE40.460C.AE96.88E9937E0FE0."],"name":[9],"type":["int"],"align":["right"]},{"label":["Ã.rzteblatt...KÃ.nstliche.Intelligenz.soll.MRT.Auswertung.beschleunigen.Default.Annotations..C_A4E56661.D66B.4EE9.9ADF.815BC159D2A3."],"name":[10],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk...Wenn.Computer.besser.diagnostizieren.als.Menschen..D_50B0166F.0307.469D.93D8.8A02818C2001."],"name":[11],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk...Wenn.Computer.besser.diagnostizieren.als.Menschen.Default.Annotations..C_8C10CDEB.7CE4.41B4.B23C.3E3F494B3B10."],"name":[12],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk.Kultur...Kann.KI.den.Krebs.besiegen..D_551EF922.7A15.48AA.A448.61D35E420341."],"name":[13],"type":["int"],"align":["right"]},{"label":["Deutschlandfunk.Kultur...Kann.KI.den.Krebs.besiegen.Default.Annotations..C_B65E3E18.3FD4.4688.B5F3.FCFF523DD9EB."],"name":[14],"type":["int"],"align":["right"]},{"label":["SWR.Wissen...KÃ.nstliche.Intelligenz.im.Kampf.gegen.Krebs..D_5E9CFFAA.5796.40AD.B298.E851D853878E."],"name":[15],"type":["int"],"align":["right"]},{"label":["SWR.Wissen...KÃ.nstliche.Intelligenz.im.Kampf.gegen.Krebs.Default.Annotations..C_AD2AD8F6.8C70.4171.812B.397311956434."],"name":[16],"type":["int"],"align":["right"]},{"label":["TK.Manager.Deutschland.steht.kurz.vor.einer.Medizin.Revolution..D_622F7E4E.DB15.44D0.BCBE.173325BE07B1."],"name":[17],"type":["int"],"align":["right"]},{"label":["TK.Manager.Deutschland.steht.kurz.vor.einer.Medizin.Revolution.Default.Annotations..C_E570D2CB.6B13.4D18.855A.DD4DC790A856."],"name":[18],"type":["int"],"align":["right"]},{"label":["Zeit...Wenn.Computer.RÃ.ntgenbilder.auswerten..D_661E6C57.3231.458F.B4F1.7F9DB5AAEE25."],"name":[19],"type":["int"],"align":["right"]},{"label":["Zeit...Wenn.Computer.RÃ.ntgenbilder.auswerten.Default.Annotations..C_8CBE585D.52ED.44EE.A984.BF6BFEB8E62B."],"name":[20],"type":["int"],"align":["right"]},{"label":["Zeit...Dr.KI.hat.nun.Zeit.fÃ.r.Sie..D_6AA35A82.E135.47DD.AB7A.008B67D15B0E."],"name":[21],"type":["int"],"align":["right"]},{"label":["Zeit...Dr.KI.hat.nun.Zeit.fÃ.r.Sie.Default.Annotations..C_402EE761.2697.4E30.B05F.04046F1995FA."],"name":[22],"type":["int"],"align":["right"]},{"label":["rnd...KI.im.Krankenhaus..D_75DF8484.5689.482A.A4C4.06D81ADD649A."],"name":[23],"type":["int"],"align":["right"]},{"label":["rnd...KI.im.Krankenhaus.Default.Annotations..C_4AB9B1D6.4E13.437B.8257.FCFE0CB2359C."],"name":[24],"type":["int"],"align":["right"]},{"label":["DW...KI.in.der.Medizin.Der.Computer.weiÃŸ..was.dir.fehlt..D_782539D2.C020.4FCA.B096.85E1384F4FDC."],"name":[25],"type":["int"],"align":["right"]},{"label":["DW...KI.in.der.Medizin.Der.Computer.weiÃŸ..was.dir.fehlt.Default.Annotations..C_62D98048.BCAD.4808.AEEE.246654551355."],"name":[26],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.hilft..Schizophrenie.besser.zu.verstehen..D_846F9002.59FC.463A.9AE0.0CA686B9D867."],"name":[27],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.hilft..Schizophrenie.besser.zu.verstehen.Default.Annotations..C_74759368.F765.46C3.BEDD.E6DD50E848BC."],"name":[28],"type":["int"],"align":["right"]},{"label":["Studie.zeigt.groÃŸes.Potenzial.in.KI.Kooperation..D_869C3658.45CB.4BF1.A748.32D3C2347443."],"name":[29],"type":["int"],"align":["right"]},{"label":["Studie.zeigt.groÃŸes.Potenzial.in.KI.Kooperation.Default.Annotations..C_157C6721.E653.47C4.AD47.293D5F0C5E07."],"name":[30],"type":["int"],"align":["right"]},{"label":["Dr..Algorithmus.Wie.kÃ.nstliche.Intelligenz.Krebspatienten.helfen.kann..D_904F3385.A505.4D75.9EB2.2B3AF23A15F5."],"name":[31],"type":["int"],"align":["right"]},{"label":["Dr..Algorithmus.Wie.kÃ.nstliche.Intelligenz.Krebspatienten.helfen.kann.Default.Annotations..C_268506AD.F993.4107.B860.89771F5FE0B7."],"name":[32],"type":["int"],"align":["right"]},{"label":["Prostatakrebs...Ultraschall.und.KÃ.nstliche.Intelligenz.liefern.Spitzenergebnisse.bei.Diagnostik..D_918CFCBD.897A.43CF.82DA.3A0775DE7706."],"name":[33],"type":["int"],"align":["right"]},{"label":["Prostatakrebs...Ultraschall.und.KÃ.nstliche.Intelligenz.liefern.Spitzenergebnisse.bei.Diagnostik.Default.Annotations..C_8C66AA16.EC22.4184.9049.AADB295313B0."],"name":[34],"type":["int"],"align":["right"]},{"label":["Arzt.versus.Computer.Wer.erkennt.Brustkrebsmetastasen.am.besten..D_A0EA56C8.D28B.4CD6.854B.3113D9E70AF2."],"name":[35],"type":["int"],"align":["right"]},{"label":["Ã.rtzeblatt...Arzt.versus.Computer..Wer.erkennt.Brustkrebsmetastasen.am.besten....C_C6FAAC3F.85B5.4C8B.8B6A.935292E74D23."],"name":[36],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.erÃ.ffnet.neue.AnsÃ.tze.in.der.Psychiatrie..D_A7B9FBD0.2287.4EDA.8CAB.D8D7950E27C0."],"name":[37],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.erÃ.ffnet.neue.AnsÃ.tze.in.der.Psychiatrie.Default.Annotations..C_4576201F.29D9.42D7.BDDF.7CFD25F6C567."],"name":[38],"type":["int"],"align":["right"]},{"label":["bz...Wie.KI.den.Krebs.besiegen.soll..D_BD7AEC40.7C16.4B8A.86E7.9782B8986536."],"name":[39],"type":["int"],"align":["right"]},{"label":["bz...Wie.KI.den.Krebs.besiegen.soll.Default.Annotations..C_B84163BD.91B9.4BF0.900A.4BBB6C177570."],"name":[40],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.fÃ.r.Ã.rzte.und.Patienten.Googeln.war.gestern..D_BE8A8EE1.EACC.49F3.8DA1.D9D24854E966."],"name":[41],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.fÃ.r.Ã.rzte.und.Patienten.Googeln.war.gestern.Default.Annotations..C_56251606.835A.4BD2.899D.2E2D4E5AD5F1."],"name":[42],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.kann.Ã.rzten.bei.Analyse.von.RÃ.ntgenbildern.helfen..D_CA3397A2.4CAE.48CF.B882.387F9B0E461D."],"name":[43],"type":["int"],"align":["right"]},{"label":["KÃ.nstliche.Intelligenz.kann.Ã.rzten.bei.Analyse.von.RÃ.ntgenbildern.helfen.Default.Annotations..C_DABBC3E5.8ECB.41B7.BD60.BFF0AF43752F."],"name":[44],"type":["int"],"align":["right"]},{"label":["Welt...Dr.Algorithmus..D_DE860A69.4DC8.4E9B.9DC1.C78F1B5BD5AF."],"name":[45],"type":["int"],"align":["right"]},{"label":["Welt...Dr.Algorithmus.Default.Annotations..C_58DE592B.5EFF.456E.96A4.9715194C78DA."],"name":[46],"type":["int"],"align":["right"]},{"label":["Diagnosen.von.Watson..D_E557C93E.4148.47DE.A0C9.C2220DCA9AB8."],"name":[47],"type":["int"],"align":["right"]},{"label":["Diagnosen.von.Watson.Default.Annotations..C_0B35B448.4683.45B0.8B23.49FCAF75C3D1."],"name":[48],"type":["int"],"align":["right"]},{"label":["Ein.Arzt.fordert.Wir.mÃ.ssen.Computer.mit.den.WÃ.nschen.der.Patienten.fÃ.ttern..D_F52964CF.D23F.4DC2.A324.38454F6E7CA3."],"name":[49],"type":["int"],"align":["right"]},{"label":["Ein.Arzt.fordert.Wir.mÃ.ssen.Computer.mit.den.WÃ.nschen.der.Patienten.fÃ.ttern.Default.Annotations..C_7DAEB684.C412.4F0C.AB16.6E362421836D."],"name":[50],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","27":"NA","28":"NA","29":"NA","30":"NA","31":"NA","32":"NA","33":"NA","34":"NA","35":"1","36":"1","37":"1","38":"1","39":"NA","40":"NA","41":"NA","42":"NA","43":"NA","44":"NA","45":"NA","46":"NA","47":"1","48":"1","49":"NA","50":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"1","27":"NA","28":"NA","29":"NA","30":"NA","31":"NA","32":"NA","33":"1","34":"1","35":"NA","36":"NA","37":"NA","38":"NA","39":"NA","40":"NA","41":"1","42":"1","43":"NA","44":"NA","45":"NA","46":"NA","47":"NA","48":"NA","49":"NA","50":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"1","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","27":"1","28":"1","29":"NA","30":"NA","31":"1","32":"1","33":"NA","34":"NA","35":"NA","36":"NA","37":"NA","38":"NA","39":"NA","40":"NA","41":"NA","42":"NA","43":"1","44":"1","45":"1","46":"1","47":"NA","48":"NA","49":"1","50":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"1","5":"NA","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"1","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","27":"NA","28":"NA","29":"1","30":"1","31":"NA","32":"NA","33":"NA","34":"NA","35":"NA","36":"NA","37":"NA","38":"NA","39":"1","40":"1","41":"NA","42":"NA","43":"NA","44":"NA","45":"NA","46":"NA","47":"NA","48":"NA","49":"NA","50":"NA","_rn_":"4"},{"1":"/Algorithm","2":"48","3":"9","4":"9","5":"2","6":"2","7":"1","8":"1","9":"NA","10":"NA","11":"9","12":"9","13":"NA","14":"NA","15":"6","16":"6","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","27":"NA","28":"NA","29":"NA","30":"NA","31":"1","32":"1","33":"NA","34":"NA","35":"4","36":"4","37":"NA","38":"NA","39":"NA","40":"NA","41":"1","42":"1","43":"NA","44":"NA","45":"7","46":"7","47":"NA","48":"NA","49":"8","50":"8","_rn_":"5"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"NA","6":"NA","7":"1","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"2","18":"2","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","27":"NA","28":"NA","29":"1","30":"1","31":"NA","32":"NA","33":"NA","34":"NA","35":"NA","36":"NA","37":"1","38":"1","39":"NA","40":"NA","41":"2","42":"2","43":"NA","44":"NA","45":"4","46":"4","47":"NA","48":"NA","49":"NA","50":"NA","_rn_":"6"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
CATMA <- CATMA %>% rename("Tags" = 1)

# delete every second column (every article has 2 columns with the exact same content)
df <- CATMA %>% select(everything()[c(TRUE, FALSE)])
df <- df[-1]

data <- cbind(CATMA[1:2],df)
# replace article names with numbers for better overview 
# (names are not relevant for our quantitative analyses)
columns <- c("Tags", "Total", c(1:24))
names(data) <- columns
data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Algorithm","2":"48","3":"9","4":"2","5":"1","6":"NA","7":"9","8":"NA","9":"6","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"4","20":"NA","21":"NA","22":"1","23":"NA","24":"7","25":"NA","26":"8"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"2","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"NA","24":"4","25":"NA","26":"NA"},{"1":"/Big Data","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"2","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Brain","2":"3","3":"NA","4":"NA","5":"3","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Chatbot","2":"18","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"2","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"16","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Cloud","2":"3","3":"NA","4":"NA","5":"2","6":"NA","7":"1","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Commentary","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA"},{"1":"/Computer","2":"69","3":"NA","4":"8","5":"NA","6":"NA","7":"10","8":"3","9":"3","10":"NA","11":"1","12":"3","13":"1","14":"3","15":"NA","16":"NA","17":"9","18":"NA","19":"6","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"1","26":"19"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"1","10":"NA","11":"1","12":"2","13":"1","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"2","24":"2","25":"1","26":"NA"},{"1":"/Digitalization","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"3","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Interview","2":"4","3":"NA","4":"1","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1"},{"1":"/Machine","2":"21","3":"NA","4":"1","5":"6","6":"NA","7":"NA","8":"1","9":"1","10":"NA","11":"NA","12":"2","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"2","22":"1","23":"NA","24":"3","25":"2","26":"NA"},{"1":"/Machine Learning","2":"2","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA"},{"1":"/Product","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"3","25":"NA","26":"NA"},{"1":"/Program","2":"6","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"3","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/Report","2":"19","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"1","12":"1","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"1","21":"1","22":"1","23":"1","24":"1","25":"NA","26":"NA"},{"1":"/Software","2":"34","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"8","9":"NA","10":"NA","11":"NA","12":"14","13":"2","14":"NA","15":"1","16":"NA","17":"NA","18":"NA","19":"4","20":"NA","21":"3","22":"NA","23":"NA","24":"1","25":"NA","26":"NA"},{"1":"/Solution","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA"},{"1":"/System","2":"68","3":"NA","4":"6","5":"NA","6":"NA","7":"2","8":"2","9":"5","10":"NA","11":"1","12":"2","13":"13","14":"NA","15":"NA","16":"1","17":"11","18":"NA","19":"NA","20":"NA","21":"2","22":"9","23":"6","24":"3","25":"NA","26":"5"},{"1":"/Technology","2":"23","3":"NA","4":"1","5":"3","6":"NA","7":"NA","8":"1","9":"NA","10":"2","11":"1","12":"NA","13":"1","14":"3","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"4","23":"NA","24":"3","25":"NA","26":"2"},{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12"},{"1":"/demands","2":"44","3":"3","4":"1","5":"2","6":"NA","7":"5","8":"1","9":"2","10":"7","11":"1","12":"1","13":"1","14":"NA","15":"NA","16":"1","17":"4","18":"NA","19":"NA","20":"1","21":"NA","22":"4","23":"NA","24":"3","25":"3","26":"4"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1"},{"1":"/opportunity","2":"112","3":"NA","4":"2","5":"6","6":"1","7":"7","8":"2","9":"5","10":"6","11":"2","12":"3","13":"6","14":"7","15":"2","16":"6","17":"8","18":"NA","19":"3","20":"2","21":"9","22":"10","23":"9","24":"14","25":"1","26":"1"},{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA"},{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA"},{"1":"/strength","2":"59","3":"NA","4":"1","5":"2","6":"NA","7":"2","8":"4","9":"3","10":"3","11":"2","12":"1","13":"4","14":"8","15":"NA","16":"1","17":"2","18":"3","19":"3","20":"NA","21":"2","22":"1","23":"2","24":"10","25":"3","26":"2"},{"1":"/threat","2":"26","3":"1","4":"1","5":"3","6":"NA","7":"5","8":"NA","9":"NA","10":"3","11":"NA","12":"1","13":"1","14":"NA","15":"NA","16":"2","17":"2","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"2","25":"1","26":"2"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA"},{"1":"/weakness","2":"60","3":"2","4":"5","5":"1","6":"1","7":"3","8":"NA","9":"6","10":"2","11":"1","12":"3","13":"4","14":"NA","15":"NA","16":"2","17":"5","18":"NA","19":"NA","20":"NA","21":"5","22":"2","23":"2","24":"4","25":"2","26":"10"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract year data
year_data <- data[1:4,]
year_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract synonym data
synonym_data <- data[c(5:10,12:14,16:19,21:24),]
synonym_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/Algorithm","2":"48","3":"9","4":"2","5":"1","6":"NA","7":"9","8":"NA","9":"6","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"4","20":"NA","21":"NA","22":"1","23":"NA","24":"7","25":"NA","26":"8","_rn_":"5"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"2","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"NA","24":"4","25":"NA","26":"NA","_rn_":"6"},{"1":"/Big Data","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"2","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"7"},{"1":"/Brain","2":"3","3":"NA","4":"NA","5":"3","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"8"},{"1":"/Chatbot","2":"18","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"2","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"16","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"9"},{"1":"/Cloud","2":"3","3":"NA","4":"NA","5":"2","6":"NA","7":"1","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"10"},{"1":"/Computer","2":"69","3":"NA","4":"8","5":"NA","6":"NA","7":"10","8":"3","9":"3","10":"NA","11":"1","12":"3","13":"1","14":"3","15":"NA","16":"NA","17":"9","18":"NA","19":"6","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"1","26":"19","_rn_":"12"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"1","10":"NA","11":"1","12":"2","13":"1","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"2","24":"2","25":"1","26":"NA","_rn_":"13"},{"1":"/Digitalization","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"3","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"14"},{"1":"/Machine","2":"21","3":"NA","4":"1","5":"6","6":"NA","7":"NA","8":"1","9":"1","10":"NA","11":"NA","12":"2","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"2","22":"1","23":"NA","24":"3","25":"2","26":"NA","_rn_":"16"},{"1":"/Machine Learning","2":"2","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"17"},{"1":"/Product","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"3","25":"NA","26":"NA","_rn_":"18"},{"1":"/Program","2":"6","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"3","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"19"},{"1":"/Software","2":"34","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"8","9":"NA","10":"NA","11":"NA","12":"14","13":"2","14":"NA","15":"1","16":"NA","17":"NA","18":"NA","19":"4","20":"NA","21":"3","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"21"},{"1":"/Solution","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"22"},{"1":"/System","2":"68","3":"NA","4":"6","5":"NA","6":"NA","7":"2","8":"2","9":"5","10":"NA","11":"1","12":"2","13":"13","14":"NA","15":"NA","16":"1","17":"11","18":"NA","19":"NA","20":"NA","21":"2","22":"9","23":"6","24":"3","25":"NA","26":"5","_rn_":"23"},{"1":"/Technology","2":"23","3":"NA","4":"1","5":"3","6":"NA","7":"NA","8":"1","9":"NA","10":"2","11":"1","12":"NA","13":"1","14":"3","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"4","23":"NA","24":"3","25":"NA","26":"2","_rn_":"24"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract article type data
article_type_data <- data[c(11,15,20),]
article_type_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/Commentary","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"11"},{"1":"/Interview","2":"4","3":"NA","4":"1","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"15"},{"1":"/Report","2":"19","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"1","12":"1","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"1","21":"1","22":"1","23":"1","24":"1","25":"NA","26":"NA","_rn_":"20"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract illness data
illness_data <- data[c(25,31,35),]
illness_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1","_rn_":"25"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1","_rn_":"31"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"35"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract sentiment data
sentiment_data <- data[c(34,30,26),]
sentiment_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4","_rn_":"34"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4","_rn_":"30"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12","_rn_":"26"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract personal impression data
personal_impression_data <- data[c(33,29,28),]
personal_impression_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract article specialization data
specialization_data <- data[c(36:38,41:43),]
specialization_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# from that, extract author expertise data
expert_data <- specialization_data[c(2,3,5,6),]
expert_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract SWOT data
SWOT_data <- data[c(39,44,32,40),]
SWOT_data
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/strength","2":"59","3":"NA","4":"1","5":"2","6":"NA","7":"2","8":"4","9":"3","10":"3","11":"2","12":"1","13":"4","14":"8","15":"NA","16":"1","17":"2","18":"3","19":"3","20":"NA","21":"2","22":"1","23":"2","24":"10","25":"3","26":"2","_rn_":"39"},{"1":"/weakness","2":"60","3":"2","4":"5","5":"1","6":"1","7":"3","8":"NA","9":"6","10":"2","11":"1","12":"3","13":"4","14":"NA","15":"NA","16":"2","17":"5","18":"NA","19":"NA","20":"NA","21":"5","22":"2","23":"2","24":"4","25":"2","26":"10","_rn_":"44"},{"1":"/opportunity","2":"112","3":"NA","4":"2","5":"6","6":"1","7":"7","8":"2","9":"5","10":"6","11":"2","12":"3","13":"6","14":"7","15":"2","16":"6","17":"8","18":"NA","19":"3","20":"2","21":"9","22":"10","23":"9","24":"14","25":"1","26":"1","_rn_":"32"},{"1":"/threat","2":"26","3":"1","4":"1","5":"3","6":"NA","7":"5","8":"NA","9":"NA","10":"3","11":"NA","12":"1","13":"1","14":"NA","15":"NA","16":"2","17":"2","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"2","25":"1","26":"2","_rn_":"40"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

# article specialization

## article specialization total

``` r
specialized_unspecialized <- specialization_data[c(1,4),]

ggplot(specialized_unspecialized, aes(fill=Tags, y=Total, x=Tags)) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count") +
    theme(legend.position = "none")
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## percentage of experts

``` r
# clean up author expertise data, calculate the number of unknown authors
specialization <- tibble("Tags" = specialization_data$Tags,
                         "Article" = c(rep("specialized", 3), rep("unspecialized", 3)),
                         "Author" = c(rep(c("unknown","expert medicine", "non-expert"), 2)),
                         "Total" = c(as.integer(specialization_data$Total[1]-
                                                specialization_data$Total[2]-
                                                specialization_data$Total[3]),
                                     specialization_data$Total[2],
                                     specialization_data$Total[3],
                                     as.integer(specialization_data$Total[4]-
                                                specialization_data$Total[5]-
                                                specialization_data$Total[6]),
                                     specialization_data$Total[5],
                                     specialization_data$Total[6]))
specialization <- cbind(specialization, specialization_data[3:26])
specialization
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Article"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Author"],"name":[3],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[4],"type":["int"],"align":["right"]},{"label":["1"],"name":[5],"type":["int"],"align":["right"]},{"label":["2"],"name":[6],"type":["int"],"align":["right"]},{"label":["3"],"name":[7],"type":["int"],"align":["right"]},{"label":["4"],"name":[8],"type":["int"],"align":["right"]},{"label":["5"],"name":[9],"type":["int"],"align":["right"]},{"label":["6"],"name":[10],"type":["int"],"align":["right"]},{"label":["7"],"name":[11],"type":["int"],"align":["right"]},{"label":["8"],"name":[12],"type":["int"],"align":["right"]},{"label":["9"],"name":[13],"type":["int"],"align":["right"]},{"label":["10"],"name":[14],"type":["int"],"align":["right"]},{"label":["11"],"name":[15],"type":["int"],"align":["right"]},{"label":["12"],"name":[16],"type":["int"],"align":["right"]},{"label":["13"],"name":[17],"type":["int"],"align":["right"]},{"label":["14"],"name":[18],"type":["int"],"align":["right"]},{"label":["15"],"name":[19],"type":["int"],"align":["right"]},{"label":["16"],"name":[20],"type":["int"],"align":["right"]},{"label":["17"],"name":[21],"type":["int"],"align":["right"]},{"label":["18"],"name":[22],"type":["int"],"align":["right"]},{"label":["19"],"name":[23],"type":["int"],"align":["right"]},{"label":["20"],"name":[24],"type":["int"],"align":["right"]},{"label":["21"],"name":[25],"type":["int"],"align":["right"]},{"label":["22"],"name":[26],"type":["int"],"align":["right"]},{"label":["23"],"name":[27],"type":["int"],"align":["right"]},{"label":["24"],"name":[28],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"specialized","3":"unknown","4":"5","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"1","19":"NA","20":"1","21":"1","22":"1","23":"NA","24":"1","25":"NA","26":"NA","27":"NA","28":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"specialized","3":"expert medicine","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","27":"NA","28":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"specialized","3":"non-expert","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","27":"NA","28":"NA","_rn_":"38"},{"1":"/unspecialized","2":"unspecialized","3":"unknown","4":"3","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"1","16":"1","17":"NA","18":"NA","19":"1","20":"NA","21":"NA","22":"NA","23":"1","24":"NA","25":"1","26":"1","27":"1","28":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"unspecialized","3":"expert medicine","4":"3","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","27":"NA","28":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"unspecialized","3":"non-expert","4":"11","5":"1","6":"NA","7":"1","8":"NA","9":"1","10":"1","11":"1","12":"1","13":"NA","14":"1","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"NA","25":"NA","26":"1","27":"1","28":"NA","_rn_":"43"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(specialization, aes(fill=Author, y=Total, x=Article)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage", x = "Article Specialization",
         fill = "Author Expertise") +
    scale_fill_manual(values=c("sienna2", "rosybrown3", "ivory3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

# article type total

``` r
ggplot(article_type_data, aes(fill=Tags, y=Total, x=Tags)) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count") +
    theme(legend.position = "none") +
    scale_fill_manual(values=c("maroon","hotpink4","deeppink4"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

# sentiment

## sentiment total

``` r
ggplot(sentiment_data, aes(fill=factor(Tags,levels=c("/pro AI","/neutral","/contra AI")), y=Total, x=factor(Tags,levels=c("/pro AI","/neutral","/contra AI")))) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count", x = "Tags") +
    theme(legend.position = "none") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

## article specialization and percentage of sentiment

``` r
# combine article specialization and sentiment data
specialization_sentiment <- rbind(specialization_data, sentiment_data)
specialization_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"},{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4","_rn_":"34"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4","_rn_":"30"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12","_rn_":"26"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
specialization_sentiment <- specialization_sentiment %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
specialization_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"4","4":"1"},{"1":"/specialized","2":"7","3":"13","4":"1"},{"1":"/specialized","2":"7","3":"14","4":"1"},{"1":"/specialized","2":"7","3":"16","4":"1"},{"1":"/specialized","2":"7","3":"17","4":"1"},{"1":"/specialized","2":"7","3":"18","4":"1"},{"1":"/specialized","2":"7","3":"20","4":"1"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"20","4":"1"},{"1":"/specialized/non-expert (author)","2":"1","3":"18","4":"1"},{"1":"/unspecialized","2":"17","3":"1","4":"1"},{"1":"/unspecialized","2":"17","3":"2","4":"1"},{"1":"/unspecialized","2":"17","3":"3","4":"1"},{"1":"/unspecialized","2":"17","3":"5","4":"1"},{"1":"/unspecialized","2":"17","3":"6","4":"1"},{"1":"/unspecialized","2":"17","3":"7","4":"1"},{"1":"/unspecialized","2":"17","3":"8","4":"1"},{"1":"/unspecialized","2":"17","3":"9","4":"1"},{"1":"/unspecialized","2":"17","3":"10","4":"1"},{"1":"/unspecialized","2":"17","3":"11","4":"1"},{"1":"/unspecialized","2":"17","3":"12","4":"1"},{"1":"/unspecialized","2":"17","3":"15","4":"1"},{"1":"/unspecialized","2":"17","3":"19","4":"1"},{"1":"/unspecialized","2":"17","3":"21","4":"1"},{"1":"/unspecialized","2":"17","3":"22","4":"1"},{"1":"/unspecialized","2":"17","3":"23","4":"1"},{"1":"/unspecialized","2":"17","3":"24","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"2","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"15","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"24","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"3","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"5","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"6","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"7","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"8","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"10","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"12","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"19","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"22","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"23","4":"1"},{"1":"/pro AI","2":"126","3":"2","4":"7"},{"1":"/pro AI","2":"126","3":"3","4":"6"},{"1":"/pro AI","2":"126","3":"5","4":"4"},{"1":"/pro AI","2":"126","3":"6","4":"11"},{"1":"/pro AI","2":"126","3":"7","4":"4"},{"1":"/pro AI","2":"126","3":"8","4":"9"},{"1":"/pro AI","2":"126","3":"9","4":"1"},{"1":"/pro AI","2":"126","3":"10","4":"3"},{"1":"/pro AI","2":"126","3":"11","4":"10"},{"1":"/pro AI","2":"126","3":"12","4":"7"},{"1":"/pro AI","2":"126","3":"13","4":"2"},{"1":"/pro AI","2":"126","3":"14","4":"3"},{"1":"/pro AI","2":"126","3":"15","4":"7"},{"1":"/pro AI","2":"126","3":"16","4":"2"},{"1":"/pro AI","2":"126","3":"17","4":"4"},{"1":"/pro AI","2":"126","3":"18","4":"4"},{"1":"/pro AI","2":"126","3":"19","4":"7"},{"1":"/pro AI","2":"126","3":"20","4":"11"},{"1":"/pro AI","2":"126","3":"21","4":"4"},{"1":"/pro AI","2":"126","3":"22","4":"14"},{"1":"/pro AI","2":"126","3":"23","4":"2"},{"1":"/pro AI","2":"126","3":"24","4":"4"},{"1":"/neutral","2":"78","3":"1","4":"1"},{"1":"/neutral","2":"78","3":"2","4":"7"},{"1":"/neutral","2":"78","3":"3","4":"1"},{"1":"/neutral","2":"78","3":"4","4":"1"},{"1":"/neutral","2":"78","3":"5","4":"2"},{"1":"/neutral","2":"78","3":"7","4":"6"},{"1":"/neutral","2":"78","3":"8","4":"3"},{"1":"/neutral","2":"78","3":"9","4":"1"},{"1":"/neutral","2":"78","3":"10","4":"4"},{"1":"/neutral","2":"78","3":"11","4":"6"},{"1":"/neutral","2":"78","3":"12","4":"3"},{"1":"/neutral","2":"78","3":"13","4":"4"},{"1":"/neutral","2":"78","3":"14","4":"5"},{"1":"/neutral","2":"78","3":"19","4":"4"},{"1":"/neutral","2":"78","3":"20","4":"13"},{"1":"/neutral","2":"78","3":"21","4":"2"},{"1":"/neutral","2":"78","3":"22","4":"10"},{"1":"/neutral","2":"78","3":"23","4":"1"},{"1":"/neutral","2":"78","3":"24","4":"4"},{"1":"/contra AI","2":"35","3":"1","4":"3"},{"1":"/contra AI","2":"35","3":"2","4":"2"},{"1":"/contra AI","2":"35","3":"5","4":"2"},{"1":"/contra AI","2":"35","3":"7","4":"1"},{"1":"/contra AI","2":"35","3":"8","4":"1"},{"1":"/contra AI","2":"35","3":"9","4":"1"},{"1":"/contra AI","2":"35","3":"10","4":"3"},{"1":"/contra AI","2":"35","3":"11","4":"1"},{"1":"/contra AI","2":"35","3":"12","4":"1"},{"1":"/contra AI","2":"35","3":"15","4":"1"},{"1":"/contra AI","2":"35","3":"19","4":"1"},{"1":"/contra AI","2":"35","3":"20","4":"3"},{"1":"/contra AI","2":"35","3":"22","4":"3"},{"1":"/contra AI","2":"35","3":"24","4":"12"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
spec <- specialization_sentiment[1:40,]
sentim <- specialization_sentiment[41:95,]

# merge data based on the articles
specialization_sentiment <- merge.data.frame(spec[-2],sentim[-2],by="article")%>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Article_Specialization" = 1, "Sentiment" = 2, "Count" = 3)
specialization_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Article_Specialization"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Sentiment"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"/contra AI","3":"3"},{"1":"/specialized","2":"/neutral","3":"23"},{"1":"/specialized","2":"/pro AI","3":"26"},{"1":"/specialized/expert (author)/medicine","2":"/contra AI","3":"3"},{"1":"/specialized/expert (author)/medicine","2":"/neutral","3":"13"},{"1":"/specialized/expert (author)/medicine","2":"/pro AI","3":"11"},{"1":"/specialized/non-expert (author)","2":"/pro AI","3":"4"},{"1":"/unspecialized","2":"/contra AI","3":"32"},{"1":"/unspecialized","2":"/neutral","3":"55"},{"1":"/unspecialized","2":"/pro AI","3":"100"},{"1":"/unspecialized/expert (author)/medicine","2":"/contra AI","3":"15"},{"1":"/unspecialized/expert (author)/medicine","2":"/neutral","3":"11"},{"1":"/unspecialized/expert (author)/medicine","2":"/pro AI","3":"18"},{"1":"/unspecialized/non-expert (author)","2":"/contra AI","3":"15"},{"1":"/unspecialized/non-expert (author)","2":"/neutral","3":"35"},{"1":"/unspecialized/non-expert (author)","2":"/pro AI","3":"67"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract author expertise data
expert_sentiment <- specialization_sentiment[c(4:7,11:16),]
expert_sentiment$Article_Specialization <- c(rep("expert medicine",3),"non-expert",rep("expert medicine",3),rep("non-expert", 3))
expert_sentiment <- expert_sentiment %>% 
                    group_by(Article_Specialization, Sentiment) %>%
                    summarise_each(list(sum = sum)) %>% 
                    rename("Author" = 1, "Count" = 3)
expert_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Author"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Sentiment"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"expert medicine","2":"/contra AI","3":"18"},{"1":"expert medicine","2":"/neutral","3":"24"},{"1":"expert medicine","2":"/pro AI","3":"29"},{"1":"non-expert","2":"/contra AI","3":"15"},{"1":"non-expert","2":"/neutral","3":"35"},{"1":"non-expert","2":"/pro AI","3":"71"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(specialization_sentiment[c(1:3,8:10),], aes(fill=factor(Sentiment,levels=c("/pro AI","/neutral","/contra AI")), y=Count, x=Article_Specialization)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage", x = "Article Specialization",
         fill = "Sentiment") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

## author expertise and percentage of sentiment

``` r
ggplot(expert_sentiment, aes(fill=factor(Sentiment,levels=c("/pro AI","/neutral","/contra AI")), y=Count, x=Author)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage", x = "Author Expertise",
         fill = "Sentiment") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

## year and percentage of sentiment

``` r
# combine year and sentiment data
year_sentiment <- rbind(year_data, sentiment_data)
year_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"},{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4","_rn_":"34"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4","_rn_":"30"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12","_rn_":"26"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
year_sentiment <- year_sentiment %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
year_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"17","4":"1"},{"1":"/2017","2":"3","3":"18","4":"1"},{"1":"/2017","2":"3","3":"23","4":"1"},{"1":"/2018","2":"4","3":"10","4":"1"},{"1":"/2018","2":"4","3":"12","4":"1"},{"1":"/2018","2":"4","3":"16","4":"1"},{"1":"/2018","2":"4","3":"20","4":"1"},{"1":"/2019","2":"8","3":"2","4":"1"},{"1":"/2019","2":"8","3":"8","4":"1"},{"1":"/2019","2":"8","3":"9","4":"1"},{"1":"/2019","2":"8","3":"13","4":"1"},{"1":"/2019","2":"8","3":"15","4":"1"},{"1":"/2019","2":"8","3":"21","4":"1"},{"1":"/2019","2":"8","3":"22","4":"1"},{"1":"/2019","2":"8","3":"24","4":"1"},{"1":"/2020","2":"9","3":"1","4":"1"},{"1":"/2020","2":"9","3":"3","4":"1"},{"1":"/2020","2":"9","3":"4","4":"1"},{"1":"/2020","2":"9","3":"5","4":"1"},{"1":"/2020","2":"9","3":"6","4":"1"},{"1":"/2020","2":"9","3":"7","4":"1"},{"1":"/2020","2":"9","3":"11","4":"1"},{"1":"/2020","2":"9","3":"14","4":"1"},{"1":"/2020","2":"9","3":"19","4":"1"},{"1":"/pro AI","2":"126","3":"2","4":"7"},{"1":"/pro AI","2":"126","3":"3","4":"6"},{"1":"/pro AI","2":"126","3":"5","4":"4"},{"1":"/pro AI","2":"126","3":"6","4":"11"},{"1":"/pro AI","2":"126","3":"7","4":"4"},{"1":"/pro AI","2":"126","3":"8","4":"9"},{"1":"/pro AI","2":"126","3":"9","4":"1"},{"1":"/pro AI","2":"126","3":"10","4":"3"},{"1":"/pro AI","2":"126","3":"11","4":"10"},{"1":"/pro AI","2":"126","3":"12","4":"7"},{"1":"/pro AI","2":"126","3":"13","4":"2"},{"1":"/pro AI","2":"126","3":"14","4":"3"},{"1":"/pro AI","2":"126","3":"15","4":"7"},{"1":"/pro AI","2":"126","3":"16","4":"2"},{"1":"/pro AI","2":"126","3":"17","4":"4"},{"1":"/pro AI","2":"126","3":"18","4":"4"},{"1":"/pro AI","2":"126","3":"19","4":"7"},{"1":"/pro AI","2":"126","3":"20","4":"11"},{"1":"/pro AI","2":"126","3":"21","4":"4"},{"1":"/pro AI","2":"126","3":"22","4":"14"},{"1":"/pro AI","2":"126","3":"23","4":"2"},{"1":"/pro AI","2":"126","3":"24","4":"4"},{"1":"/neutral","2":"78","3":"1","4":"1"},{"1":"/neutral","2":"78","3":"2","4":"7"},{"1":"/neutral","2":"78","3":"3","4":"1"},{"1":"/neutral","2":"78","3":"4","4":"1"},{"1":"/neutral","2":"78","3":"5","4":"2"},{"1":"/neutral","2":"78","3":"7","4":"6"},{"1":"/neutral","2":"78","3":"8","4":"3"},{"1":"/neutral","2":"78","3":"9","4":"1"},{"1":"/neutral","2":"78","3":"10","4":"4"},{"1":"/neutral","2":"78","3":"11","4":"6"},{"1":"/neutral","2":"78","3":"12","4":"3"},{"1":"/neutral","2":"78","3":"13","4":"4"},{"1":"/neutral","2":"78","3":"14","4":"5"},{"1":"/neutral","2":"78","3":"19","4":"4"},{"1":"/neutral","2":"78","3":"20","4":"13"},{"1":"/neutral","2":"78","3":"21","4":"2"},{"1":"/neutral","2":"78","3":"22","4":"10"},{"1":"/neutral","2":"78","3":"23","4":"1"},{"1":"/neutral","2":"78","3":"24","4":"4"},{"1":"/contra AI","2":"35","3":"1","4":"3"},{"1":"/contra AI","2":"35","3":"2","4":"2"},{"1":"/contra AI","2":"35","3":"5","4":"2"},{"1":"/contra AI","2":"35","3":"7","4":"1"},{"1":"/contra AI","2":"35","3":"8","4":"1"},{"1":"/contra AI","2":"35","3":"9","4":"1"},{"1":"/contra AI","2":"35","3":"10","4":"3"},{"1":"/contra AI","2":"35","3":"11","4":"1"},{"1":"/contra AI","2":"35","3":"12","4":"1"},{"1":"/contra AI","2":"35","3":"15","4":"1"},{"1":"/contra AI","2":"35","3":"19","4":"1"},{"1":"/contra AI","2":"35","3":"20","4":"3"},{"1":"/contra AI","2":"35","3":"22","4":"3"},{"1":"/contra AI","2":"35","3":"24","4":"12"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
sentim <- year_sentiment[25:79,]
year <- year_sentiment[1:24,]

# merge data based on the articles
year_sentiment <- merge.data.frame(sentim[-2],year[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Sentiment" = 1, "Year" = 2, "Count" = 3)
year_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Sentiment"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Year"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/contra AI","2":"/2018","3":"7"},{"1":"/contra AI","2":"/2019","3":"20"},{"1":"/contra AI","2":"/2020","3":"8"},{"1":"/neutral","2":"/2017","3":"1"},{"1":"/neutral","2":"/2018","3":"20"},{"1":"/neutral","2":"/2019","3":"31"},{"1":"/neutral","2":"/2020","3":"26"},{"1":"/pro AI","2":"/2017","3":"10"},{"1":"/pro AI","2":"/2018","3":"23"},{"1":"/pro AI","2":"/2019","3":"48"},{"1":"/pro AI","2":"/2020","3":"45"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(year_sentiment, aes(fill=factor(Sentiment,levels=c("/pro AI","/neutral","/contra AI")), y=Count, x=Year)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage", x = "Year",
         fill = "Sentiment") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

## personal impression and percentage of sentiment

``` r
# combine personal impression and sentiment data
impression_sentiment <- rbind(personal_impression_data, sentiment_data)
impression_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"},{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4","_rn_":"34"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4","_rn_":"30"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12","_rn_":"26"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
impression_sentiment <- impression_sentiment %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
impression_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/positive","2":"13","3":"2","4":"1"},{"1":"/positive","2":"13","3":"6","4":"1"},{"1":"/positive","2":"13","3":"8","4":"1"},{"1":"/positive","2":"13","3":"11","4":"1"},{"1":"/positive","2":"13","3":"12","4":"1"},{"1":"/positive","2":"13","3":"13","4":"1"},{"1":"/positive","2":"13","3":"14","4":"1"},{"1":"/positive","2":"13","3":"15","4":"1"},{"1":"/positive","2":"13","3":"16","4":"1"},{"1":"/positive","2":"13","3":"17","4":"1"},{"1":"/positive","2":"13","3":"19","4":"1"},{"1":"/positive","2":"13","3":"20","4":"1"},{"1":"/positive","2":"13","3":"23","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"3","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"4","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"5","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"7","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"9","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"18","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"21","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"22","4":"1"},{"1":"/negative","2":"3","3":"1","4":"1"},{"1":"/negative","2":"3","3":"10","4":"1"},{"1":"/negative","2":"3","3":"24","4":"1"},{"1":"/pro AI","2":"126","3":"2","4":"7"},{"1":"/pro AI","2":"126","3":"3","4":"6"},{"1":"/pro AI","2":"126","3":"5","4":"4"},{"1":"/pro AI","2":"126","3":"6","4":"11"},{"1":"/pro AI","2":"126","3":"7","4":"4"},{"1":"/pro AI","2":"126","3":"8","4":"9"},{"1":"/pro AI","2":"126","3":"9","4":"1"},{"1":"/pro AI","2":"126","3":"10","4":"3"},{"1":"/pro AI","2":"126","3":"11","4":"10"},{"1":"/pro AI","2":"126","3":"12","4":"7"},{"1":"/pro AI","2":"126","3":"13","4":"2"},{"1":"/pro AI","2":"126","3":"14","4":"3"},{"1":"/pro AI","2":"126","3":"15","4":"7"},{"1":"/pro AI","2":"126","3":"16","4":"2"},{"1":"/pro AI","2":"126","3":"17","4":"4"},{"1":"/pro AI","2":"126","3":"18","4":"4"},{"1":"/pro AI","2":"126","3":"19","4":"7"},{"1":"/pro AI","2":"126","3":"20","4":"11"},{"1":"/pro AI","2":"126","3":"21","4":"4"},{"1":"/pro AI","2":"126","3":"22","4":"14"},{"1":"/pro AI","2":"126","3":"23","4":"2"},{"1":"/pro AI","2":"126","3":"24","4":"4"},{"1":"/neutral","2":"78","3":"1","4":"1"},{"1":"/neutral","2":"78","3":"2","4":"7"},{"1":"/neutral","2":"78","3":"3","4":"1"},{"1":"/neutral","2":"78","3":"4","4":"1"},{"1":"/neutral","2":"78","3":"5","4":"2"},{"1":"/neutral","2":"78","3":"7","4":"6"},{"1":"/neutral","2":"78","3":"8","4":"3"},{"1":"/neutral","2":"78","3":"9","4":"1"},{"1":"/neutral","2":"78","3":"10","4":"4"},{"1":"/neutral","2":"78","3":"11","4":"6"},{"1":"/neutral","2":"78","3":"12","4":"3"},{"1":"/neutral","2":"78","3":"13","4":"4"},{"1":"/neutral","2":"78","3":"14","4":"5"},{"1":"/neutral","2":"78","3":"19","4":"4"},{"1":"/neutral","2":"78","3":"20","4":"13"},{"1":"/neutral","2":"78","3":"21","4":"2"},{"1":"/neutral","2":"78","3":"22","4":"10"},{"1":"/neutral","2":"78","3":"23","4":"1"},{"1":"/neutral","2":"78","3":"24","4":"4"},{"1":"/contra AI","2":"35","3":"1","4":"3"},{"1":"/contra AI","2":"35","3":"2","4":"2"},{"1":"/contra AI","2":"35","3":"5","4":"2"},{"1":"/contra AI","2":"35","3":"7","4":"1"},{"1":"/contra AI","2":"35","3":"8","4":"1"},{"1":"/contra AI","2":"35","3":"9","4":"1"},{"1":"/contra AI","2":"35","3":"10","4":"3"},{"1":"/contra AI","2":"35","3":"11","4":"1"},{"1":"/contra AI","2":"35","3":"12","4":"1"},{"1":"/contra AI","2":"35","3":"15","4":"1"},{"1":"/contra AI","2":"35","3":"19","4":"1"},{"1":"/contra AI","2":"35","3":"20","4":"3"},{"1":"/contra AI","2":"35","3":"22","4":"3"},{"1":"/contra AI","2":"35","3":"24","4":"12"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
impr <- impression_sentiment[1:24,]
sentim <- impression_sentiment[25:79,]

impression_sentiment <- merge.data.frame(impr[-2],sentim[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Personal_Impression" = 1, "Sentiment" = 2, "Count" = 3)
impression_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Personal_Impression"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Sentiment"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/negative","2":"/contra AI","3":"18"},{"1":"/negative","2":"/neutral","3":"9"},{"1":"/negative","2":"/pro AI","3":"7"},{"1":"/neither positive nor negative","2":"/contra AI","3":"7"},{"1":"/neither positive nor negative","2":"/neutral","3":"23"},{"1":"/neither positive nor negative","2":"/pro AI","3":"37"},{"1":"/positive","2":"/contra AI","3":"10"},{"1":"/positive","2":"/neutral","3":"46"},{"1":"/positive","2":"/pro AI","3":"82"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(impression_sentiment, aes(fill=factor(Sentiment, levels=c("/pro AI","/neutral","/contra AI")), y=Count, x=Personal_Impression)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "Sentiment") +
    theme(plot.title = element_text(hjust = 0.5, size = 14)) +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

# personal impression

## personal impression total

``` r
ggplot(personal_impression_data, aes(fill=factor(Tags,levels=c("/positive","/neither positive nor negative","/negative")), y=Total, x=factor(Tags,levels=c("/positive","/neither positive nor negative","/negative")))) + 
    geom_bar(position="dodge", stat="identity") +
    labs(x = "Tags", y = "Count") +
    theme(legend.position = "none") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

## article specialization and percentage of personal impression

``` r
# combine article specialization and personal impression data
specialization_impression <- rbind(specialization_data, personal_impression_data)
specialization_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"},{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
specialization_impression <- specialization_impression %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
specialization_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"4","4":"1"},{"1":"/specialized","2":"7","3":"13","4":"1"},{"1":"/specialized","2":"7","3":"14","4":"1"},{"1":"/specialized","2":"7","3":"16","4":"1"},{"1":"/specialized","2":"7","3":"17","4":"1"},{"1":"/specialized","2":"7","3":"18","4":"1"},{"1":"/specialized","2":"7","3":"20","4":"1"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"20","4":"1"},{"1":"/specialized/non-expert (author)","2":"1","3":"18","4":"1"},{"1":"/unspecialized","2":"17","3":"1","4":"1"},{"1":"/unspecialized","2":"17","3":"2","4":"1"},{"1":"/unspecialized","2":"17","3":"3","4":"1"},{"1":"/unspecialized","2":"17","3":"5","4":"1"},{"1":"/unspecialized","2":"17","3":"6","4":"1"},{"1":"/unspecialized","2":"17","3":"7","4":"1"},{"1":"/unspecialized","2":"17","3":"8","4":"1"},{"1":"/unspecialized","2":"17","3":"9","4":"1"},{"1":"/unspecialized","2":"17","3":"10","4":"1"},{"1":"/unspecialized","2":"17","3":"11","4":"1"},{"1":"/unspecialized","2":"17","3":"12","4":"1"},{"1":"/unspecialized","2":"17","3":"15","4":"1"},{"1":"/unspecialized","2":"17","3":"19","4":"1"},{"1":"/unspecialized","2":"17","3":"21","4":"1"},{"1":"/unspecialized","2":"17","3":"22","4":"1"},{"1":"/unspecialized","2":"17","3":"23","4":"1"},{"1":"/unspecialized","2":"17","3":"24","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"2","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"15","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"24","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"3","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"5","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"6","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"7","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"8","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"10","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"12","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"19","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"22","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"23","4":"1"},{"1":"/positive","2":"13","3":"2","4":"1"},{"1":"/positive","2":"13","3":"6","4":"1"},{"1":"/positive","2":"13","3":"8","4":"1"},{"1":"/positive","2":"13","3":"11","4":"1"},{"1":"/positive","2":"13","3":"12","4":"1"},{"1":"/positive","2":"13","3":"13","4":"1"},{"1":"/positive","2":"13","3":"14","4":"1"},{"1":"/positive","2":"13","3":"15","4":"1"},{"1":"/positive","2":"13","3":"16","4":"1"},{"1":"/positive","2":"13","3":"17","4":"1"},{"1":"/positive","2":"13","3":"19","4":"1"},{"1":"/positive","2":"13","3":"20","4":"1"},{"1":"/positive","2":"13","3":"23","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"3","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"4","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"5","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"7","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"9","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"18","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"21","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"22","4":"1"},{"1":"/negative","2":"3","3":"1","4":"1"},{"1":"/negative","2":"3","3":"10","4":"1"},{"1":"/negative","2":"3","3":"24","4":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
spec <- specialization_impression[c(1:40),]
impr <- specialization_impression[41:64,]

# merge data based on the articles
specialization_impression <- merge.data.frame(spec[-2],impr[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Article_Specialization" = 1, "Personal_Impression" = 2, "Count" = 3)
specialization_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Article_Specialization"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Personal_Impression"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"/neither positive nor negative","3":"2"},{"1":"/specialized","2":"/positive","3":"5"},{"1":"/specialized/expert (author)/medicine","2":"/positive","3":"1"},{"1":"/specialized/non-expert (author)","2":"/neither positive nor negative","3":"1"},{"1":"/unspecialized","2":"/negative","3":"3"},{"1":"/unspecialized","2":"/neither positive nor negative","3":"6"},{"1":"/unspecialized","2":"/positive","3":"8"},{"1":"/unspecialized/expert (author)/medicine","2":"/negative","3":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"/positive","3":"2"},{"1":"/unspecialized/non-expert (author)","2":"/negative","3":"2"},{"1":"/unspecialized/non-expert (author)","2":"/neither positive nor negative","3":"4"},{"1":"/unspecialized/non-expert (author)","2":"/positive","3":"5"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract author expertise data
expert_impression <- specialization_impression[c(3,4,8:12),]
expert_impression$Article_Specialization <- c("expert medicine","non-expert",rep("expert medicine",2),rep("non-expert",3))
expert_impression <- expert_impression %>% 
                    group_by(Article_Specialization, Personal_Impression) %>%
                    summarise_each(list(sum = sum)) %>% 
                    rename("Author" = 1, "Count" = 3)
expert_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Author"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Personal_Impression"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"expert medicine","2":"/negative","3":"1"},{"1":"expert medicine","2":"/positive","3":"3"},{"1":"non-expert","2":"/negative","3":"2"},{"1":"non-expert","2":"/neither positive nor negative","3":"5"},{"1":"non-expert","2":"/positive","3":"5"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(specialization_impression[c(1,2,5:7),], aes(fill=factor(Personal_Impression,levels=c("/positive","/neither positive nor negative","/negative")), y=Count, x=Article_Specialization)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         x = "Article Specialization",
         fill = "Personal Impression") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

## author expertise and percentage of personal impression

``` r
ggplot(expert_impression, aes(fill=factor(Personal_Impression,levels=c("/positive","/neither positive nor negative","/negative")), y=Count, x=Author)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         x = "Author Expertise",
         fill = "Personal Impression") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

## year and percentage of personal impression

``` r
# combine year and personal impression data
year_impression <- rbind(year_data, personal_impression_data)
year_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"},{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
year_impression <- year_impression %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
year_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"17","4":"1"},{"1":"/2017","2":"3","3":"18","4":"1"},{"1":"/2017","2":"3","3":"23","4":"1"},{"1":"/2018","2":"4","3":"10","4":"1"},{"1":"/2018","2":"4","3":"12","4":"1"},{"1":"/2018","2":"4","3":"16","4":"1"},{"1":"/2018","2":"4","3":"20","4":"1"},{"1":"/2019","2":"8","3":"2","4":"1"},{"1":"/2019","2":"8","3":"8","4":"1"},{"1":"/2019","2":"8","3":"9","4":"1"},{"1":"/2019","2":"8","3":"13","4":"1"},{"1":"/2019","2":"8","3":"15","4":"1"},{"1":"/2019","2":"8","3":"21","4":"1"},{"1":"/2019","2":"8","3":"22","4":"1"},{"1":"/2019","2":"8","3":"24","4":"1"},{"1":"/2020","2":"9","3":"1","4":"1"},{"1":"/2020","2":"9","3":"3","4":"1"},{"1":"/2020","2":"9","3":"4","4":"1"},{"1":"/2020","2":"9","3":"5","4":"1"},{"1":"/2020","2":"9","3":"6","4":"1"},{"1":"/2020","2":"9","3":"7","4":"1"},{"1":"/2020","2":"9","3":"11","4":"1"},{"1":"/2020","2":"9","3":"14","4":"1"},{"1":"/2020","2":"9","3":"19","4":"1"},{"1":"/positive","2":"13","3":"2","4":"1"},{"1":"/positive","2":"13","3":"6","4":"1"},{"1":"/positive","2":"13","3":"8","4":"1"},{"1":"/positive","2":"13","3":"11","4":"1"},{"1":"/positive","2":"13","3":"12","4":"1"},{"1":"/positive","2":"13","3":"13","4":"1"},{"1":"/positive","2":"13","3":"14","4":"1"},{"1":"/positive","2":"13","3":"15","4":"1"},{"1":"/positive","2":"13","3":"16","4":"1"},{"1":"/positive","2":"13","3":"17","4":"1"},{"1":"/positive","2":"13","3":"19","4":"1"},{"1":"/positive","2":"13","3":"20","4":"1"},{"1":"/positive","2":"13","3":"23","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"3","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"4","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"5","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"7","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"9","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"18","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"21","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"22","4":"1"},{"1":"/negative","2":"3","3":"1","4":"1"},{"1":"/negative","2":"3","3":"10","4":"1"},{"1":"/negative","2":"3","3":"24","4":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
impr <- year_impression[25:48,]
year <- year_impression[1:24,]

# merge data based on the articles
year_impression <- merge.data.frame(impr[-2],year[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Personal_Impression" = 1, "Year" = 2, "Count" = 3)
year_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Personal_Impression"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Year"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/negative","2":"/2018","3":"1"},{"1":"/negative","2":"/2019","3":"1"},{"1":"/negative","2":"/2020","3":"1"},{"1":"/neither positive nor negative","2":"/2017","3":"1"},{"1":"/neither positive nor negative","2":"/2019","3":"3"},{"1":"/neither positive nor negative","2":"/2020","3":"4"},{"1":"/positive","2":"/2017","3":"2"},{"1":"/positive","2":"/2018","3":"3"},{"1":"/positive","2":"/2019","3":"4"},{"1":"/positive","2":"/2020","3":"4"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(year_impression, aes(fill=factor(Personal_Impression,levels=c("/positive","/neither positive nor negative","/negative")), y=Count, x=Year)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "Personal Impression") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

# SWOT

## SWOT total

``` r
ggplot(SWOT_data, aes(fill=factor(Tags, levels=c("/strength","/weakness","/opportunity","/threat")), y=Total, x=factor(Tags, levels=c("/strength","/weakness","/opportunity","/threat")))) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count",
         x = "Tags") +
    theme(legend.position = "none") +
    scale_fill_manual(values=c("deeppink3","cadetblue2","coral1","red3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

## article specialization and percentage of SWOT

``` r
# combine article specialization and SWOT data
specialization_SWOT <- rbind(specialization_data, SWOT_data)
specialization_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"},{"1":"/strength","2":"59","3":"NA","4":"1","5":"2","6":"NA","7":"2","8":"4","9":"3","10":"3","11":"2","12":"1","13":"4","14":"8","15":"NA","16":"1","17":"2","18":"3","19":"3","20":"NA","21":"2","22":"1","23":"2","24":"10","25":"3","26":"2","_rn_":"39"},{"1":"/weakness","2":"60","3":"2","4":"5","5":"1","6":"1","7":"3","8":"NA","9":"6","10":"2","11":"1","12":"3","13":"4","14":"NA","15":"NA","16":"2","17":"5","18":"NA","19":"NA","20":"NA","21":"5","22":"2","23":"2","24":"4","25":"2","26":"10","_rn_":"44"},{"1":"/opportunity","2":"112","3":"NA","4":"2","5":"6","6":"1","7":"7","8":"2","9":"5","10":"6","11":"2","12":"3","13":"6","14":"7","15":"2","16":"6","17":"8","18":"NA","19":"3","20":"2","21":"9","22":"10","23":"9","24":"14","25":"1","26":"1","_rn_":"32"},{"1":"/threat","2":"26","3":"1","4":"1","5":"3","6":"NA","7":"5","8":"NA","9":"NA","10":"3","11":"NA","12":"1","13":"1","14":"NA","15":"NA","16":"2","17":"2","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"2","25":"1","26":"2","_rn_":"40"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
specialization_SWOT <- specialization_SWOT %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
specialization_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"4","4":"1"},{"1":"/specialized","2":"7","3":"13","4":"1"},{"1":"/specialized","2":"7","3":"14","4":"1"},{"1":"/specialized","2":"7","3":"16","4":"1"},{"1":"/specialized","2":"7","3":"17","4":"1"},{"1":"/specialized","2":"7","3":"18","4":"1"},{"1":"/specialized","2":"7","3":"20","4":"1"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"20","4":"1"},{"1":"/specialized/non-expert (author)","2":"1","3":"18","4":"1"},{"1":"/unspecialized","2":"17","3":"1","4":"1"},{"1":"/unspecialized","2":"17","3":"2","4":"1"},{"1":"/unspecialized","2":"17","3":"3","4":"1"},{"1":"/unspecialized","2":"17","3":"5","4":"1"},{"1":"/unspecialized","2":"17","3":"6","4":"1"},{"1":"/unspecialized","2":"17","3":"7","4":"1"},{"1":"/unspecialized","2":"17","3":"8","4":"1"},{"1":"/unspecialized","2":"17","3":"9","4":"1"},{"1":"/unspecialized","2":"17","3":"10","4":"1"},{"1":"/unspecialized","2":"17","3":"11","4":"1"},{"1":"/unspecialized","2":"17","3":"12","4":"1"},{"1":"/unspecialized","2":"17","3":"15","4":"1"},{"1":"/unspecialized","2":"17","3":"19","4":"1"},{"1":"/unspecialized","2":"17","3":"21","4":"1"},{"1":"/unspecialized","2":"17","3":"22","4":"1"},{"1":"/unspecialized","2":"17","3":"23","4":"1"},{"1":"/unspecialized","2":"17","3":"24","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"2","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"15","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"24","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"3","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"5","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"6","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"7","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"8","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"10","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"12","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"19","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"22","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"23","4":"1"},{"1":"/strength","2":"59","3":"2","4":"1"},{"1":"/strength","2":"59","3":"3","4":"2"},{"1":"/strength","2":"59","3":"5","4":"2"},{"1":"/strength","2":"59","3":"6","4":"4"},{"1":"/strength","2":"59","3":"7","4":"3"},{"1":"/strength","2":"59","3":"8","4":"3"},{"1":"/strength","2":"59","3":"9","4":"2"},{"1":"/strength","2":"59","3":"10","4":"1"},{"1":"/strength","2":"59","3":"11","4":"4"},{"1":"/strength","2":"59","3":"12","4":"8"},{"1":"/strength","2":"59","3":"14","4":"1"},{"1":"/strength","2":"59","3":"15","4":"2"},{"1":"/strength","2":"59","3":"16","4":"3"},{"1":"/strength","2":"59","3":"17","4":"3"},{"1":"/strength","2":"59","3":"19","4":"2"},{"1":"/strength","2":"59","3":"20","4":"1"},{"1":"/strength","2":"59","3":"21","4":"2"},{"1":"/strength","2":"59","3":"22","4":"10"},{"1":"/strength","2":"59","3":"23","4":"3"},{"1":"/strength","2":"59","3":"24","4":"2"},{"1":"/weakness","2":"60","3":"1","4":"2"},{"1":"/weakness","2":"60","3":"2","4":"5"},{"1":"/weakness","2":"60","3":"3","4":"1"},{"1":"/weakness","2":"60","3":"4","4":"1"},{"1":"/weakness","2":"60","3":"5","4":"3"},{"1":"/weakness","2":"60","3":"7","4":"6"},{"1":"/weakness","2":"60","3":"8","4":"2"},{"1":"/weakness","2":"60","3":"9","4":"1"},{"1":"/weakness","2":"60","3":"10","4":"3"},{"1":"/weakness","2":"60","3":"11","4":"4"},{"1":"/weakness","2":"60","3":"14","4":"2"},{"1":"/weakness","2":"60","3":"15","4":"5"},{"1":"/weakness","2":"60","3":"19","4":"5"},{"1":"/weakness","2":"60","3":"20","4":"2"},{"1":"/weakness","2":"60","3":"21","4":"2"},{"1":"/weakness","2":"60","3":"22","4":"4"},{"1":"/weakness","2":"60","3":"23","4":"2"},{"1":"/weakness","2":"60","3":"24","4":"10"},{"1":"/opportunity","2":"112","3":"2","4":"2"},{"1":"/opportunity","2":"112","3":"3","4":"6"},{"1":"/opportunity","2":"112","3":"4","4":"1"},{"1":"/opportunity","2":"112","3":"5","4":"7"},{"1":"/opportunity","2":"112","3":"6","4":"2"},{"1":"/opportunity","2":"112","3":"7","4":"5"},{"1":"/opportunity","2":"112","3":"8","4":"6"},{"1":"/opportunity","2":"112","3":"9","4":"2"},{"1":"/opportunity","2":"112","3":"10","4":"3"},{"1":"/opportunity","2":"112","3":"11","4":"6"},{"1":"/opportunity","2":"112","3":"12","4":"7"},{"1":"/opportunity","2":"112","3":"13","4":"2"},{"1":"/opportunity","2":"112","3":"14","4":"6"},{"1":"/opportunity","2":"112","3":"15","4":"8"},{"1":"/opportunity","2":"112","3":"17","4":"3"},{"1":"/opportunity","2":"112","3":"18","4":"2"},{"1":"/opportunity","2":"112","3":"19","4":"9"},{"1":"/opportunity","2":"112","3":"20","4":"10"},{"1":"/opportunity","2":"112","3":"21","4":"9"},{"1":"/opportunity","2":"112","3":"22","4":"14"},{"1":"/opportunity","2":"112","3":"23","4":"1"},{"1":"/opportunity","2":"112","3":"24","4":"1"},{"1":"/threat","2":"26","3":"1","4":"1"},{"1":"/threat","2":"26","3":"2","4":"1"},{"1":"/threat","2":"26","3":"3","4":"3"},{"1":"/threat","2":"26","3":"5","4":"5"},{"1":"/threat","2":"26","3":"8","4":"3"},{"1":"/threat","2":"26","3":"10","4":"1"},{"1":"/threat","2":"26","3":"11","4":"1"},{"1":"/threat","2":"26","3":"14","4":"2"},{"1":"/threat","2":"26","3":"15","4":"2"},{"1":"/threat","2":"26","3":"20","4":"2"},{"1":"/threat","2":"26","3":"22","4":"2"},{"1":"/threat","2":"26","3":"23","4":"1"},{"1":"/threat","2":"26","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
spec <- specialization_SWOT[c(1:40),]
swot <- specialization_SWOT[41:113,]

# merge data based on the articles
specialization_SWOT <- merge.data.frame(spec[-2],swot[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Article_Specialization" = 1, "SWOT" = 2, "Count" = 3)
specialization_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Article_Specialization"],"name":[1],"type":["chr"],"align":["left"]},{"label":["SWOT"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"/opportunity","3":"24"},{"1":"/specialized","2":"/strength","3":"8"},{"1":"/specialized","2":"/threat","3":"4"},{"1":"/specialized","2":"/weakness","3":"5"},{"1":"/specialized/expert (author)/medicine","2":"/opportunity","3":"10"},{"1":"/specialized/expert (author)/medicine","2":"/strength","3":"1"},{"1":"/specialized/expert (author)/medicine","2":"/threat","3":"2"},{"1":"/specialized/expert (author)/medicine","2":"/weakness","3":"2"},{"1":"/specialized/non-expert (author)","2":"/opportunity","3":"2"},{"1":"/unspecialized","2":"/opportunity","3":"88"},{"1":"/unspecialized","2":"/strength","3":"51"},{"1":"/unspecialized","2":"/threat","3":"22"},{"1":"/unspecialized","2":"/weakness","3":"55"},{"1":"/unspecialized/expert (author)/medicine","2":"/opportunity","3":"11"},{"1":"/unspecialized/expert (author)/medicine","2":"/strength","3":"5"},{"1":"/unspecialized/expert (author)/medicine","2":"/threat","3":"5"},{"1":"/unspecialized/expert (author)/medicine","2":"/weakness","3":"20"},{"1":"/unspecialized/non-expert (author)","2":"/opportunity","3":"60"},{"1":"/unspecialized/non-expert (author)","2":"/strength","3":"38"},{"1":"/unspecialized/non-expert (author)","2":"/threat","3":"16"},{"1":"/unspecialized/non-expert (author)","2":"/weakness","3":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract author expertise data
expert_SWOT <- specialization_SWOT[c(5:9,14:21),]
expert_SWOT$Article_Specialization <- c(rep("expert medicine",4),"non-expert",rep("expert medicine",4),rep("non-expert",4))
expert_SWOT <- expert_SWOT %>% 
                    group_by(Article_Specialization, SWOT) %>%
                    summarise_each(list(sum = sum)) %>% 
                    rename("Author" = 1, "Count" = 3)
expert_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Author"],"name":[1],"type":["chr"],"align":["left"]},{"label":["SWOT"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"expert medicine","2":"/opportunity","3":"21"},{"1":"expert medicine","2":"/strength","3":"6"},{"1":"expert medicine","2":"/threat","3":"7"},{"1":"expert medicine","2":"/weakness","3":"22"},{"1":"non-expert","2":"/opportunity","3":"62"},{"1":"non-expert","2":"/strength","3":"38"},{"1":"non-expert","2":"/threat","3":"16"},{"1":"non-expert","2":"/weakness","3":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(specialization_SWOT[c(1:4,10:13),], aes(fill=factor(SWOT, levels=c("/strength","/weakness","/opportunity","/threat")), y=Count, x=Article_Specialization)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         x = "Article Specialization",
         fill = "SWOT") +
    scale_fill_manual(values=c("deeppink3","cadetblue2","coral1","red3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

## author expertise and percentage of SWOT

``` r
ggplot(expert_SWOT, aes(fill=factor(SWOT, levels=c("/strength","/weakness","/opportunity","/threat")), y=Count, x=Author)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         x = "Author Expertise",
         fill = "SWOT") +
    scale_fill_manual(values=c("deeppink3","cadetblue2","coral1","red3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

## year and percentage of SWOT

``` r
# combine year and SWOT data
year_SWOT <- rbind(year_data, SWOT_data)
year_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"},{"1":"/strength","2":"59","3":"NA","4":"1","5":"2","6":"NA","7":"2","8":"4","9":"3","10":"3","11":"2","12":"1","13":"4","14":"8","15":"NA","16":"1","17":"2","18":"3","19":"3","20":"NA","21":"2","22":"1","23":"2","24":"10","25":"3","26":"2","_rn_":"39"},{"1":"/weakness","2":"60","3":"2","4":"5","5":"1","6":"1","7":"3","8":"NA","9":"6","10":"2","11":"1","12":"3","13":"4","14":"NA","15":"NA","16":"2","17":"5","18":"NA","19":"NA","20":"NA","21":"5","22":"2","23":"2","24":"4","25":"2","26":"10","_rn_":"44"},{"1":"/opportunity","2":"112","3":"NA","4":"2","5":"6","6":"1","7":"7","8":"2","9":"5","10":"6","11":"2","12":"3","13":"6","14":"7","15":"2","16":"6","17":"8","18":"NA","19":"3","20":"2","21":"9","22":"10","23":"9","24":"14","25":"1","26":"1","_rn_":"32"},{"1":"/threat","2":"26","3":"1","4":"1","5":"3","6":"NA","7":"5","8":"NA","9":"NA","10":"3","11":"NA","12":"1","13":"1","14":"NA","15":"NA","16":"2","17":"2","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"2","25":"1","26":"2","_rn_":"40"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
year_SWOT <- year_SWOT %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
year_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"17","4":"1"},{"1":"/2017","2":"3","3":"18","4":"1"},{"1":"/2017","2":"3","3":"23","4":"1"},{"1":"/2018","2":"4","3":"10","4":"1"},{"1":"/2018","2":"4","3":"12","4":"1"},{"1":"/2018","2":"4","3":"16","4":"1"},{"1":"/2018","2":"4","3":"20","4":"1"},{"1":"/2019","2":"8","3":"2","4":"1"},{"1":"/2019","2":"8","3":"8","4":"1"},{"1":"/2019","2":"8","3":"9","4":"1"},{"1":"/2019","2":"8","3":"13","4":"1"},{"1":"/2019","2":"8","3":"15","4":"1"},{"1":"/2019","2":"8","3":"21","4":"1"},{"1":"/2019","2":"8","3":"22","4":"1"},{"1":"/2019","2":"8","3":"24","4":"1"},{"1":"/2020","2":"9","3":"1","4":"1"},{"1":"/2020","2":"9","3":"3","4":"1"},{"1":"/2020","2":"9","3":"4","4":"1"},{"1":"/2020","2":"9","3":"5","4":"1"},{"1":"/2020","2":"9","3":"6","4":"1"},{"1":"/2020","2":"9","3":"7","4":"1"},{"1":"/2020","2":"9","3":"11","4":"1"},{"1":"/2020","2":"9","3":"14","4":"1"},{"1":"/2020","2":"9","3":"19","4":"1"},{"1":"/strength","2":"59","3":"2","4":"1"},{"1":"/strength","2":"59","3":"3","4":"2"},{"1":"/strength","2":"59","3":"5","4":"2"},{"1":"/strength","2":"59","3":"6","4":"4"},{"1":"/strength","2":"59","3":"7","4":"3"},{"1":"/strength","2":"59","3":"8","4":"3"},{"1":"/strength","2":"59","3":"9","4":"2"},{"1":"/strength","2":"59","3":"10","4":"1"},{"1":"/strength","2":"59","3":"11","4":"4"},{"1":"/strength","2":"59","3":"12","4":"8"},{"1":"/strength","2":"59","3":"14","4":"1"},{"1":"/strength","2":"59","3":"15","4":"2"},{"1":"/strength","2":"59","3":"16","4":"3"},{"1":"/strength","2":"59","3":"17","4":"3"},{"1":"/strength","2":"59","3":"19","4":"2"},{"1":"/strength","2":"59","3":"20","4":"1"},{"1":"/strength","2":"59","3":"21","4":"2"},{"1":"/strength","2":"59","3":"22","4":"10"},{"1":"/strength","2":"59","3":"23","4":"3"},{"1":"/strength","2":"59","3":"24","4":"2"},{"1":"/weakness","2":"60","3":"1","4":"2"},{"1":"/weakness","2":"60","3":"2","4":"5"},{"1":"/weakness","2":"60","3":"3","4":"1"},{"1":"/weakness","2":"60","3":"4","4":"1"},{"1":"/weakness","2":"60","3":"5","4":"3"},{"1":"/weakness","2":"60","3":"7","4":"6"},{"1":"/weakness","2":"60","3":"8","4":"2"},{"1":"/weakness","2":"60","3":"9","4":"1"},{"1":"/weakness","2":"60","3":"10","4":"3"},{"1":"/weakness","2":"60","3":"11","4":"4"},{"1":"/weakness","2":"60","3":"14","4":"2"},{"1":"/weakness","2":"60","3":"15","4":"5"},{"1":"/weakness","2":"60","3":"19","4":"5"},{"1":"/weakness","2":"60","3":"20","4":"2"},{"1":"/weakness","2":"60","3":"21","4":"2"},{"1":"/weakness","2":"60","3":"22","4":"4"},{"1":"/weakness","2":"60","3":"23","4":"2"},{"1":"/weakness","2":"60","3":"24","4":"10"},{"1":"/opportunity","2":"112","3":"2","4":"2"},{"1":"/opportunity","2":"112","3":"3","4":"6"},{"1":"/opportunity","2":"112","3":"4","4":"1"},{"1":"/opportunity","2":"112","3":"5","4":"7"},{"1":"/opportunity","2":"112","3":"6","4":"2"},{"1":"/opportunity","2":"112","3":"7","4":"5"},{"1":"/opportunity","2":"112","3":"8","4":"6"},{"1":"/opportunity","2":"112","3":"9","4":"2"},{"1":"/opportunity","2":"112","3":"10","4":"3"},{"1":"/opportunity","2":"112","3":"11","4":"6"},{"1":"/opportunity","2":"112","3":"12","4":"7"},{"1":"/opportunity","2":"112","3":"13","4":"2"},{"1":"/opportunity","2":"112","3":"14","4":"6"},{"1":"/opportunity","2":"112","3":"15","4":"8"},{"1":"/opportunity","2":"112","3":"17","4":"3"},{"1":"/opportunity","2":"112","3":"18","4":"2"},{"1":"/opportunity","2":"112","3":"19","4":"9"},{"1":"/opportunity","2":"112","3":"20","4":"10"},{"1":"/opportunity","2":"112","3":"21","4":"9"},{"1":"/opportunity","2":"112","3":"22","4":"14"},{"1":"/opportunity","2":"112","3":"23","4":"1"},{"1":"/opportunity","2":"112","3":"24","4":"1"},{"1":"/threat","2":"26","3":"1","4":"1"},{"1":"/threat","2":"26","3":"2","4":"1"},{"1":"/threat","2":"26","3":"3","4":"3"},{"1":"/threat","2":"26","3":"5","4":"5"},{"1":"/threat","2":"26","3":"8","4":"3"},{"1":"/threat","2":"26","3":"10","4":"1"},{"1":"/threat","2":"26","3":"11","4":"1"},{"1":"/threat","2":"26","3":"14","4":"2"},{"1":"/threat","2":"26","3":"15","4":"2"},{"1":"/threat","2":"26","3":"20","4":"2"},{"1":"/threat","2":"26","3":"22","4":"2"},{"1":"/threat","2":"26","3":"23","4":"1"},{"1":"/threat","2":"26","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
swot <- year_SWOT[25:97,]
year <- year_SWOT[1:24,]

# merge data based on the articles
year_SWOT <- merge.data.frame(swot[-2],year[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("SWOT" = 1, "Year" = 2, "Count" = 3)
year_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["SWOT"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Year"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/opportunity","2":"/2017","3":"6"},{"1":"/opportunity","2":"/2018","3":"20"},{"1":"/opportunity","2":"/2019","3":"44"},{"1":"/opportunity","2":"/2020","3":"42"},{"1":"/strength","2":"/2017","3":"6"},{"1":"/strength","2":"/2018","3":"13"},{"1":"/strength","2":"/2019","3":"22"},{"1":"/strength","2":"/2020","3":"18"},{"1":"/threat","2":"/2017","3":"1"},{"1":"/threat","2":"/2018","3":"3"},{"1":"/threat","2":"/2019","3":"10"},{"1":"/threat","2":"/2020","3":"12"},{"1":"/weakness","2":"/2017","3":"2"},{"1":"/weakness","2":"/2018","3":"5"},{"1":"/weakness","2":"/2019","3":"29"},{"1":"/weakness","2":"/2020","3":"24"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(year_SWOT, aes(fill=factor(SWOT, levels=c("/strength","/weakness","/opportunity","/threat")), y=Count, x=Year)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "SWOT") +
    scale_fill_manual(values=c("deeppink3","cadetblue2","coral1","red3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

# synonyms

## synonyms total

``` r
ggplot(synonym_data, aes(fill=Tags, y=Total, x=Tags)) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count",
         x = "Tags") +
    theme(axis.text.x=element_text(angle=90,hjust=1),
          legend.position = "none")
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

## article specialization and percentage of synonyms

``` r
# combine article specialization and synonym data
specialization_synonyms <- rbind(specialization_data, synonym_data)
specialization_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"1","16":"1","17":"NA","18":"1","19":"1","20":"1","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"36"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"37"},{"1":"/specialized/non-expert (author)","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"38"},{"1":"/unspecialized","2":"17","3":"1","4":"1","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"1","12":"1","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"1","24":"1","25":"1","26":"1","_rn_":"41"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"42"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"NA","5":"1","6":"NA","7":"1","8":"1","9":"1","10":"1","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"1","25":"1","26":"NA","_rn_":"43"},{"1":"/Algorithm","2":"48","3":"9","4":"2","5":"1","6":"NA","7":"9","8":"NA","9":"6","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"4","20":"NA","21":"NA","22":"1","23":"NA","24":"7","25":"NA","26":"8","_rn_":"5"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"2","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"NA","24":"4","25":"NA","26":"NA","_rn_":"6"},{"1":"/Big Data","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"2","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"7"},{"1":"/Brain","2":"3","3":"NA","4":"NA","5":"3","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"8"},{"1":"/Chatbot","2":"18","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"2","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"16","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"9"},{"1":"/Cloud","2":"3","3":"NA","4":"NA","5":"2","6":"NA","7":"1","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"10"},{"1":"/Computer","2":"69","3":"NA","4":"8","5":"NA","6":"NA","7":"10","8":"3","9":"3","10":"NA","11":"1","12":"3","13":"1","14":"3","15":"NA","16":"NA","17":"9","18":"NA","19":"6","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"1","26":"19","_rn_":"12"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"1","10":"NA","11":"1","12":"2","13":"1","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"2","24":"2","25":"1","26":"NA","_rn_":"13"},{"1":"/Digitalization","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"3","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"14"},{"1":"/Machine","2":"21","3":"NA","4":"1","5":"6","6":"NA","7":"NA","8":"1","9":"1","10":"NA","11":"NA","12":"2","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"2","22":"1","23":"NA","24":"3","25":"2","26":"NA","_rn_":"16"},{"1":"/Machine Learning","2":"2","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"17"},{"1":"/Product","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"3","25":"NA","26":"NA","_rn_":"18"},{"1":"/Program","2":"6","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"3","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"19"},{"1":"/Software","2":"34","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"8","9":"NA","10":"NA","11":"NA","12":"14","13":"2","14":"NA","15":"1","16":"NA","17":"NA","18":"NA","19":"4","20":"NA","21":"3","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"21"},{"1":"/Solution","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"22"},{"1":"/System","2":"68","3":"NA","4":"6","5":"NA","6":"NA","7":"2","8":"2","9":"5","10":"NA","11":"1","12":"2","13":"13","14":"NA","15":"NA","16":"1","17":"11","18":"NA","19":"NA","20":"NA","21":"2","22":"9","23":"6","24":"3","25":"NA","26":"5","_rn_":"23"},{"1":"/Technology","2":"23","3":"NA","4":"1","5":"3","6":"NA","7":"NA","8":"1","9":"NA","10":"2","11":"1","12":"NA","13":"1","14":"3","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"4","23":"NA","24":"3","25":"NA","26":"2","_rn_":"24"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
specialization_synonyms <- specialization_synonyms %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
specialization_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"7","3":"4","4":"1"},{"1":"/specialized","2":"7","3":"13","4":"1"},{"1":"/specialized","2":"7","3":"14","4":"1"},{"1":"/specialized","2":"7","3":"16","4":"1"},{"1":"/specialized","2":"7","3":"17","4":"1"},{"1":"/specialized","2":"7","3":"18","4":"1"},{"1":"/specialized","2":"7","3":"20","4":"1"},{"1":"/specialized/expert (author)/medicine","2":"1","3":"20","4":"1"},{"1":"/specialized/non-expert (author)","2":"1","3":"18","4":"1"},{"1":"/unspecialized","2":"17","3":"1","4":"1"},{"1":"/unspecialized","2":"17","3":"2","4":"1"},{"1":"/unspecialized","2":"17","3":"3","4":"1"},{"1":"/unspecialized","2":"17","3":"5","4":"1"},{"1":"/unspecialized","2":"17","3":"6","4":"1"},{"1":"/unspecialized","2":"17","3":"7","4":"1"},{"1":"/unspecialized","2":"17","3":"8","4":"1"},{"1":"/unspecialized","2":"17","3":"9","4":"1"},{"1":"/unspecialized","2":"17","3":"10","4":"1"},{"1":"/unspecialized","2":"17","3":"11","4":"1"},{"1":"/unspecialized","2":"17","3":"12","4":"1"},{"1":"/unspecialized","2":"17","3":"15","4":"1"},{"1":"/unspecialized","2":"17","3":"19","4":"1"},{"1":"/unspecialized","2":"17","3":"21","4":"1"},{"1":"/unspecialized","2":"17","3":"22","4":"1"},{"1":"/unspecialized","2":"17","3":"23","4":"1"},{"1":"/unspecialized","2":"17","3":"24","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"2","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"15","4":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"3","3":"24","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"1","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"3","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"5","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"6","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"7","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"8","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"10","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"12","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"19","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"22","4":"1"},{"1":"/unspecialized/non-expert (author)","2":"11","3":"23","4":"1"},{"1":"/Algorithm","2":"48","3":"1","4":"9"},{"1":"/Algorithm","2":"48","3":"2","4":"2"},{"1":"/Algorithm","2":"48","3":"3","4":"1"},{"1":"/Algorithm","2":"48","3":"5","4":"9"},{"1":"/Algorithm","2":"48","3":"7","4":"6"},{"1":"/Algorithm","2":"48","3":"15","4":"1"},{"1":"/Algorithm","2":"48","3":"17","4":"4"},{"1":"/Algorithm","2":"48","3":"20","4":"1"},{"1":"/Algorithm","2":"48","3":"22","4":"7"},{"1":"/Algorithm","2":"48","3":"24","4":"8"},{"1":"/Application","2":"11","3":"3","4":"1"},{"1":"/Application","2":"11","3":"8","4":"2"},{"1":"/Application","2":"11","3":"14","4":"1"},{"1":"/Application","2":"11","3":"18","4":"1"},{"1":"/Application","2":"11","3":"20","4":"2"},{"1":"/Application","2":"11","3":"22","4":"4"},{"1":"/Big Data","2":"5","3":"5","4":"2"},{"1":"/Big Data","2":"5","3":"12","4":"1"},{"1":"/Big Data","2":"5","3":"20","4":"2"},{"1":"/Brain","2":"3","3":"3","4":"3"},{"1":"/Chatbot","2":"18","3":"12","4":"2"},{"1":"/Chatbot","2":"18","3":"20","4":"16"},{"1":"/Cloud","2":"3","3":"3","4":"2"},{"1":"/Cloud","2":"3","3":"5","4":"1"},{"1":"/Computer","2":"69","3":"2","4":"8"},{"1":"/Computer","2":"69","3":"5","4":"10"},{"1":"/Computer","2":"69","3":"6","4":"3"},{"1":"/Computer","2":"69","3":"7","4":"3"},{"1":"/Computer","2":"69","3":"9","4":"1"},{"1":"/Computer","2":"69","3":"10","4":"3"},{"1":"/Computer","2":"69","3":"11","4":"1"},{"1":"/Computer","2":"69","3":"12","4":"3"},{"1":"/Computer","2":"69","3":"15","4":"9"},{"1":"/Computer","2":"69","3":"17","4":"6"},{"1":"/Computer","2":"69","3":"21","4":"1"},{"1":"/Computer","2":"69","3":"22","4":"1"},{"1":"/Computer","2":"69","3":"23","4":"1"},{"1":"/Computer","2":"69","3":"24","4":"19"},{"1":"/Deep Learning / Networks","2":"20","3":"1","4":"7"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"9","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"10","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"11","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"18","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"20","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"21","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"22","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"23","4":"1"},{"1":"/Digitalization","2":"5","3":"5","4":"3"},{"1":"/Digitalization","2":"5","3":"6","4":"1"},{"1":"/Digitalization","2":"5","3":"8","4":"1"},{"1":"/Machine","2":"21","3":"2","4":"1"},{"1":"/Machine","2":"21","3":"3","4":"6"},{"1":"/Machine","2":"21","3":"6","4":"1"},{"1":"/Machine","2":"21","3":"7","4":"1"},{"1":"/Machine","2":"21","3":"10","4":"2"},{"1":"/Machine","2":"21","3":"12","4":"1"},{"1":"/Machine","2":"21","3":"17","4":"1"},{"1":"/Machine","2":"21","3":"19","4":"2"},{"1":"/Machine","2":"21","3":"20","4":"1"},{"1":"/Machine","2":"21","3":"22","4":"3"},{"1":"/Machine","2":"21","3":"23","4":"2"},{"1":"/Machine Learning","2":"2","3":"18","4":"1"},{"1":"/Machine Learning","2":"2","3":"23","4":"1"},{"1":"/Product","2":"3","3":"22","4":"3"},{"1":"/Program","2":"6","3":"4","4":"1"},{"1":"/Program","2":"6","3":"10","4":"3"},{"1":"/Program","2":"6","3":"17","4":"1"},{"1":"/Program","2":"6","3":"19","4":"1"},{"1":"/Software","2":"34","3":"3","4":"1"},{"1":"/Software","2":"34","3":"6","4":"8"},{"1":"/Software","2":"34","3":"10","4":"14"},{"1":"/Software","2":"34","3":"11","4":"2"},{"1":"/Software","2":"34","3":"13","4":"1"},{"1":"/Software","2":"34","3":"17","4":"4"},{"1":"/Software","2":"34","3":"19","4":"3"},{"1":"/Software","2":"34","3":"22","4":"1"},{"1":"/Solution","2":"1","3":"22","4":"1"},{"1":"/System","2":"68","3":"2","4":"6"},{"1":"/System","2":"68","3":"5","4":"2"},{"1":"/System","2":"68","3":"6","4":"2"},{"1":"/System","2":"68","3":"7","4":"5"},{"1":"/System","2":"68","3":"9","4":"1"},{"1":"/System","2":"68","3":"10","4":"2"},{"1":"/System","2":"68","3":"11","4":"13"},{"1":"/System","2":"68","3":"14","4":"1"},{"1":"/System","2":"68","3":"15","4":"11"},{"1":"/System","2":"68","3":"19","4":"2"},{"1":"/System","2":"68","3":"20","4":"9"},{"1":"/System","2":"68","3":"21","4":"6"},{"1":"/System","2":"68","3":"22","4":"3"},{"1":"/System","2":"68","3":"24","4":"5"},{"1":"/Technology","2":"23","3":"2","4":"1"},{"1":"/Technology","2":"23","3":"3","4":"3"},{"1":"/Technology","2":"23","3":"6","4":"1"},{"1":"/Technology","2":"23","3":"8","4":"2"},{"1":"/Technology","2":"23","3":"9","4":"1"},{"1":"/Technology","2":"23","3":"11","4":"1"},{"1":"/Technology","2":"23","3":"12","4":"3"},{"1":"/Technology","2":"23","3":"15","4":"1"},{"1":"/Technology","2":"23","3":"19","4":"1"},{"1":"/Technology","2":"23","3":"20","4":"4"},{"1":"/Technology","2":"23","3":"22","4":"3"},{"1":"/Technology","2":"23","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
spec <- specialization_synonyms[1:40,]
syn <- specialization_synonyms[41:144,]

# merge data based on the articles
specialization_synonyms<- merge.data.frame(spec[-2],syn[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Article_Specialization" = 1, "Synonyms" = 2, "Count" = 3)
specialization_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Article_Specialization"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Synonyms"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/specialized","2":"/Algorithm","3":"5"},{"1":"/specialized","2":"/Application","3":"4"},{"1":"/specialized","2":"/Big Data","3":"2"},{"1":"/specialized","2":"/Chatbot","3":"16"},{"1":"/specialized","2":"/Computer","3":"6"},{"1":"/specialized","2":"/Deep Learning / Networks","3":"3"},{"1":"/specialized","2":"/Machine","3":"2"},{"1":"/specialized","2":"/Machine Learning","3":"1"},{"1":"/specialized","2":"/Program","3":"2"},{"1":"/specialized","2":"/Software","3":"5"},{"1":"/specialized","2":"/System","3":"10"},{"1":"/specialized","2":"/Technology","3":"4"},{"1":"/specialized/expert (author)/medicine","2":"/Algorithm","3":"1"},{"1":"/specialized/expert (author)/medicine","2":"/Application","3":"2"},{"1":"/specialized/expert (author)/medicine","2":"/Big Data","3":"2"},{"1":"/specialized/expert (author)/medicine","2":"/Chatbot","3":"16"},{"1":"/specialized/expert (author)/medicine","2":"/Deep Learning / Networks","3":"2"},{"1":"/specialized/expert (author)/medicine","2":"/Machine","3":"1"},{"1":"/specialized/expert (author)/medicine","2":"/System","3":"9"},{"1":"/specialized/expert (author)/medicine","2":"/Technology","3":"4"},{"1":"/specialized/non-expert (author)","2":"/Application","3":"1"},{"1":"/specialized/non-expert (author)","2":"/Deep Learning / Networks","3":"1"},{"1":"/specialized/non-expert (author)","2":"/Machine Learning","3":"1"},{"1":"/unspecialized","2":"/Algorithm","3":"43"},{"1":"/unspecialized","2":"/Application","3":"7"},{"1":"/unspecialized","2":"/Big Data","3":"3"},{"1":"/unspecialized","2":"/Brain","3":"3"},{"1":"/unspecialized","2":"/Chatbot","3":"2"},{"1":"/unspecialized","2":"/Cloud","3":"3"},{"1":"/unspecialized","2":"/Computer","3":"63"},{"1":"/unspecialized","2":"/Deep Learning / Networks","3":"17"},{"1":"/unspecialized","2":"/Digitalization","3":"5"},{"1":"/unspecialized","2":"/Machine","3":"19"},{"1":"/unspecialized","2":"/Machine Learning","3":"1"},{"1":"/unspecialized","2":"/Product","3":"3"},{"1":"/unspecialized","2":"/Program","3":"4"},{"1":"/unspecialized","2":"/Software","3":"29"},{"1":"/unspecialized","2":"/Solution","3":"1"},{"1":"/unspecialized","2":"/System","3":"58"},{"1":"/unspecialized","2":"/Technology","3":"19"},{"1":"/unspecialized/expert (author)/medicine","2":"/Algorithm","3":"11"},{"1":"/unspecialized/expert (author)/medicine","2":"/Computer","3":"36"},{"1":"/unspecialized/expert (author)/medicine","2":"/Machine","3":"1"},{"1":"/unspecialized/expert (author)/medicine","2":"/System","3":"22"},{"1":"/unspecialized/expert (author)/medicine","2":"/Technology","3":"4"},{"1":"/unspecialized/non-expert (author)","2":"/Algorithm","3":"32"},{"1":"/unspecialized/non-expert (author)","2":"/Application","3":"7"},{"1":"/unspecialized/non-expert (author)","2":"/Big Data","3":"3"},{"1":"/unspecialized/non-expert (author)","2":"/Brain","3":"3"},{"1":"/unspecialized/non-expert (author)","2":"/Chatbot","3":"2"},{"1":"/unspecialized/non-expert (author)","2":"/Cloud","3":"3"},{"1":"/unspecialized/non-expert (author)","2":"/Computer","3":"24"},{"1":"/unspecialized/non-expert (author)","2":"/Deep Learning / Networks","3":"13"},{"1":"/unspecialized/non-expert (author)","2":"/Digitalization","3":"5"},{"1":"/unspecialized/non-expert (author)","2":"/Machine","3":"18"},{"1":"/unspecialized/non-expert (author)","2":"/Machine Learning","3":"1"},{"1":"/unspecialized/non-expert (author)","2":"/Product","3":"3"},{"1":"/unspecialized/non-expert (author)","2":"/Program","3":"4"},{"1":"/unspecialized/non-expert (author)","2":"/Software","3":"27"},{"1":"/unspecialized/non-expert (author)","2":"/Solution","3":"1"},{"1":"/unspecialized/non-expert (author)","2":"/System","3":"16"},{"1":"/unspecialized/non-expert (author)","2":"/Technology","3":"13"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# extract author expertise data
expert_synonyms <- specialization_synonyms[c(13:23,41:62),]
expert_synonyms$Article_Specialization <- c(rep("expert medicine",8),rep("non-expert",3),rep("expert medicine",5),rep("non-expert",17))
expert_synonyms <- expert_synonyms %>% 
                    group_by(Article_Specialization, Synonyms) %>%
                    summarise_each(list(sum = sum)) %>% 
                    rename("Author" = 1, "Count" = 3)
expert_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Author"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Synonyms"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"expert medicine","2":"/Algorithm","3":"12"},{"1":"expert medicine","2":"/Application","3":"2"},{"1":"expert medicine","2":"/Big Data","3":"2"},{"1":"expert medicine","2":"/Chatbot","3":"16"},{"1":"expert medicine","2":"/Computer","3":"36"},{"1":"expert medicine","2":"/Deep Learning / Networks","3":"2"},{"1":"expert medicine","2":"/Machine","3":"2"},{"1":"expert medicine","2":"/System","3":"31"},{"1":"expert medicine","2":"/Technology","3":"8"},{"1":"non-expert","2":"/Algorithm","3":"32"},{"1":"non-expert","2":"/Application","3":"8"},{"1":"non-expert","2":"/Big Data","3":"3"},{"1":"non-expert","2":"/Brain","3":"3"},{"1":"non-expert","2":"/Chatbot","3":"2"},{"1":"non-expert","2":"/Cloud","3":"3"},{"1":"non-expert","2":"/Computer","3":"24"},{"1":"non-expert","2":"/Deep Learning / Networks","3":"14"},{"1":"non-expert","2":"/Digitalization","3":"5"},{"1":"non-expert","2":"/Machine","3":"18"},{"1":"non-expert","2":"/Machine Learning","3":"2"},{"1":"non-expert","2":"/Product","3":"3"},{"1":"non-expert","2":"/Program","3":"4"},{"1":"non-expert","2":"/Software","3":"27"},{"1":"non-expert","2":"/Solution","3":"1"},{"1":"non-expert","2":"/System","3":"16"},{"1":"non-expert","2":"/Technology","3":"13"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(specialization_synonyms[c(1:12,24:40),], aes(fill=Synonyms, y=Count, x=Article_Specialization)) + 
    geom_bar(position="fill", stat="identity", color="black") +
    labs(title = "",
         y = "Percentage",
         x = "Article Specialization")
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

## author expertise and percentage of synonyms

``` r
ggplot(expert_synonyms, aes(fill=Synonyms, y=Count, x=Author)) + 
    geom_bar(position="fill", stat="identity", color = "black") +
    labs(title = "",
         y = "Percentage",
         x = "Author Expertise")
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

## year and count of synonyms

``` r
# combine year and synonym data
year_synonyms <- rbind(year_data, synonym_data)
year_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"},{"1":"/Algorithm","2":"48","3":"9","4":"2","5":"1","6":"NA","7":"9","8":"NA","9":"6","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"4","20":"NA","21":"NA","22":"1","23":"NA","24":"7","25":"NA","26":"8","_rn_":"5"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"2","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"NA","24":"4","25":"NA","26":"NA","_rn_":"6"},{"1":"/Big Data","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"2","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"7"},{"1":"/Brain","2":"3","3":"NA","4":"NA","5":"3","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"8"},{"1":"/Chatbot","2":"18","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"2","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"16","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"9"},{"1":"/Cloud","2":"3","3":"NA","4":"NA","5":"2","6":"NA","7":"1","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"10"},{"1":"/Computer","2":"69","3":"NA","4":"8","5":"NA","6":"NA","7":"10","8":"3","9":"3","10":"NA","11":"1","12":"3","13":"1","14":"3","15":"NA","16":"NA","17":"9","18":"NA","19":"6","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"1","26":"19","_rn_":"12"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"1","10":"NA","11":"1","12":"2","13":"1","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"2","24":"2","25":"1","26":"NA","_rn_":"13"},{"1":"/Digitalization","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"3","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"14"},{"1":"/Machine","2":"21","3":"NA","4":"1","5":"6","6":"NA","7":"NA","8":"1","9":"1","10":"NA","11":"NA","12":"2","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"2","22":"1","23":"NA","24":"3","25":"2","26":"NA","_rn_":"16"},{"1":"/Machine Learning","2":"2","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"17"},{"1":"/Product","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"3","25":"NA","26":"NA","_rn_":"18"},{"1":"/Program","2":"6","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"3","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"19"},{"1":"/Software","2":"34","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"8","9":"NA","10":"NA","11":"NA","12":"14","13":"2","14":"NA","15":"1","16":"NA","17":"NA","18":"NA","19":"4","20":"NA","21":"3","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"21"},{"1":"/Solution","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"22"},{"1":"/System","2":"68","3":"NA","4":"6","5":"NA","6":"NA","7":"2","8":"2","9":"5","10":"NA","11":"1","12":"2","13":"13","14":"NA","15":"NA","16":"1","17":"11","18":"NA","19":"NA","20":"NA","21":"2","22":"9","23":"6","24":"3","25":"NA","26":"5","_rn_":"23"},{"1":"/Technology","2":"23","3":"NA","4":"1","5":"3","6":"NA","7":"NA","8":"1","9":"NA","10":"2","11":"1","12":"NA","13":"1","14":"3","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"4","23":"NA","24":"3","25":"NA","26":"2","_rn_":"24"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
year_synonyms <- year_synonyms %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
year_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"17","4":"1"},{"1":"/2017","2":"3","3":"18","4":"1"},{"1":"/2017","2":"3","3":"23","4":"1"},{"1":"/2018","2":"4","3":"10","4":"1"},{"1":"/2018","2":"4","3":"12","4":"1"},{"1":"/2018","2":"4","3":"16","4":"1"},{"1":"/2018","2":"4","3":"20","4":"1"},{"1":"/2019","2":"8","3":"2","4":"1"},{"1":"/2019","2":"8","3":"8","4":"1"},{"1":"/2019","2":"8","3":"9","4":"1"},{"1":"/2019","2":"8","3":"13","4":"1"},{"1":"/2019","2":"8","3":"15","4":"1"},{"1":"/2019","2":"8","3":"21","4":"1"},{"1":"/2019","2":"8","3":"22","4":"1"},{"1":"/2019","2":"8","3":"24","4":"1"},{"1":"/2020","2":"9","3":"1","4":"1"},{"1":"/2020","2":"9","3":"3","4":"1"},{"1":"/2020","2":"9","3":"4","4":"1"},{"1":"/2020","2":"9","3":"5","4":"1"},{"1":"/2020","2":"9","3":"6","4":"1"},{"1":"/2020","2":"9","3":"7","4":"1"},{"1":"/2020","2":"9","3":"11","4":"1"},{"1":"/2020","2":"9","3":"14","4":"1"},{"1":"/2020","2":"9","3":"19","4":"1"},{"1":"/Algorithm","2":"48","3":"1","4":"9"},{"1":"/Algorithm","2":"48","3":"2","4":"2"},{"1":"/Algorithm","2":"48","3":"3","4":"1"},{"1":"/Algorithm","2":"48","3":"5","4":"9"},{"1":"/Algorithm","2":"48","3":"7","4":"6"},{"1":"/Algorithm","2":"48","3":"15","4":"1"},{"1":"/Algorithm","2":"48","3":"17","4":"4"},{"1":"/Algorithm","2":"48","3":"20","4":"1"},{"1":"/Algorithm","2":"48","3":"22","4":"7"},{"1":"/Algorithm","2":"48","3":"24","4":"8"},{"1":"/Application","2":"11","3":"3","4":"1"},{"1":"/Application","2":"11","3":"8","4":"2"},{"1":"/Application","2":"11","3":"14","4":"1"},{"1":"/Application","2":"11","3":"18","4":"1"},{"1":"/Application","2":"11","3":"20","4":"2"},{"1":"/Application","2":"11","3":"22","4":"4"},{"1":"/Big Data","2":"5","3":"5","4":"2"},{"1":"/Big Data","2":"5","3":"12","4":"1"},{"1":"/Big Data","2":"5","3":"20","4":"2"},{"1":"/Brain","2":"3","3":"3","4":"3"},{"1":"/Chatbot","2":"18","3":"12","4":"2"},{"1":"/Chatbot","2":"18","3":"20","4":"16"},{"1":"/Cloud","2":"3","3":"3","4":"2"},{"1":"/Cloud","2":"3","3":"5","4":"1"},{"1":"/Computer","2":"69","3":"2","4":"8"},{"1":"/Computer","2":"69","3":"5","4":"10"},{"1":"/Computer","2":"69","3":"6","4":"3"},{"1":"/Computer","2":"69","3":"7","4":"3"},{"1":"/Computer","2":"69","3":"9","4":"1"},{"1":"/Computer","2":"69","3":"10","4":"3"},{"1":"/Computer","2":"69","3":"11","4":"1"},{"1":"/Computer","2":"69","3":"12","4":"3"},{"1":"/Computer","2":"69","3":"15","4":"9"},{"1":"/Computer","2":"69","3":"17","4":"6"},{"1":"/Computer","2":"69","3":"21","4":"1"},{"1":"/Computer","2":"69","3":"22","4":"1"},{"1":"/Computer","2":"69","3":"23","4":"1"},{"1":"/Computer","2":"69","3":"24","4":"19"},{"1":"/Deep Learning / Networks","2":"20","3":"1","4":"7"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"9","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"10","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"11","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"18","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"20","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"21","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"22","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"23","4":"1"},{"1":"/Digitalization","2":"5","3":"5","4":"3"},{"1":"/Digitalization","2":"5","3":"6","4":"1"},{"1":"/Digitalization","2":"5","3":"8","4":"1"},{"1":"/Machine","2":"21","3":"2","4":"1"},{"1":"/Machine","2":"21","3":"3","4":"6"},{"1":"/Machine","2":"21","3":"6","4":"1"},{"1":"/Machine","2":"21","3":"7","4":"1"},{"1":"/Machine","2":"21","3":"10","4":"2"},{"1":"/Machine","2":"21","3":"12","4":"1"},{"1":"/Machine","2":"21","3":"17","4":"1"},{"1":"/Machine","2":"21","3":"19","4":"2"},{"1":"/Machine","2":"21","3":"20","4":"1"},{"1":"/Machine","2":"21","3":"22","4":"3"},{"1":"/Machine","2":"21","3":"23","4":"2"},{"1":"/Machine Learning","2":"2","3":"18","4":"1"},{"1":"/Machine Learning","2":"2","3":"23","4":"1"},{"1":"/Product","2":"3","3":"22","4":"3"},{"1":"/Program","2":"6","3":"4","4":"1"},{"1":"/Program","2":"6","3":"10","4":"3"},{"1":"/Program","2":"6","3":"17","4":"1"},{"1":"/Program","2":"6","3":"19","4":"1"},{"1":"/Software","2":"34","3":"3","4":"1"},{"1":"/Software","2":"34","3":"6","4":"8"},{"1":"/Software","2":"34","3":"10","4":"14"},{"1":"/Software","2":"34","3":"11","4":"2"},{"1":"/Software","2":"34","3":"13","4":"1"},{"1":"/Software","2":"34","3":"17","4":"4"},{"1":"/Software","2":"34","3":"19","4":"3"},{"1":"/Software","2":"34","3":"22","4":"1"},{"1":"/Solution","2":"1","3":"22","4":"1"},{"1":"/System","2":"68","3":"2","4":"6"},{"1":"/System","2":"68","3":"5","4":"2"},{"1":"/System","2":"68","3":"6","4":"2"},{"1":"/System","2":"68","3":"7","4":"5"},{"1":"/System","2":"68","3":"9","4":"1"},{"1":"/System","2":"68","3":"10","4":"2"},{"1":"/System","2":"68","3":"11","4":"13"},{"1":"/System","2":"68","3":"14","4":"1"},{"1":"/System","2":"68","3":"15","4":"11"},{"1":"/System","2":"68","3":"19","4":"2"},{"1":"/System","2":"68","3":"20","4":"9"},{"1":"/System","2":"68","3":"21","4":"6"},{"1":"/System","2":"68","3":"22","4":"3"},{"1":"/System","2":"68","3":"24","4":"5"},{"1":"/Technology","2":"23","3":"2","4":"1"},{"1":"/Technology","2":"23","3":"3","4":"3"},{"1":"/Technology","2":"23","3":"6","4":"1"},{"1":"/Technology","2":"23","3":"8","4":"2"},{"1":"/Technology","2":"23","3":"9","4":"1"},{"1":"/Technology","2":"23","3":"11","4":"1"},{"1":"/Technology","2":"23","3":"12","4":"3"},{"1":"/Technology","2":"23","3":"15","4":"1"},{"1":"/Technology","2":"23","3":"19","4":"1"},{"1":"/Technology","2":"23","3":"20","4":"4"},{"1":"/Technology","2":"23","3":"22","4":"3"},{"1":"/Technology","2":"23","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
syn <- year_synonyms[25:128,]
year <- year_synonyms[1:24,]

# merge data based on the articles
year_synonyms <- merge.data.frame(syn[-2],year[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Synonyms" = 1, "Year" = 2, "Count" = 3)
year_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Synonyms"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Year"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/Algorithm","2":"/2017","3":"4"},{"1":"/Algorithm","2":"/2018","3":"1"},{"1":"/Algorithm","2":"/2019","3":"18"},{"1":"/Algorithm","2":"/2020","3":"25"},{"1":"/Application","2":"/2017","3":"1"},{"1":"/Application","2":"/2018","3":"2"},{"1":"/Application","2":"/2019","3":"6"},{"1":"/Application","2":"/2020","3":"2"},{"1":"/Big Data","2":"/2018","3":"3"},{"1":"/Big Data","2":"/2020","3":"2"},{"1":"/Brain","2":"/2020","3":"3"},{"1":"/Chatbot","2":"/2018","3":"18"},{"1":"/Cloud","2":"/2020","3":"3"},{"1":"/Computer","2":"/2017","3":"7"},{"1":"/Computer","2":"/2018","3":"6"},{"1":"/Computer","2":"/2019","3":"39"},{"1":"/Computer","2":"/2020","3":"17"},{"1":"/Deep Learning / Networks","2":"/2017","3":"2"},{"1":"/Deep Learning / Networks","2":"/2018","3":"4"},{"1":"/Deep Learning / Networks","2":"/2019","3":"5"},{"1":"/Deep Learning / Networks","2":"/2020","3":"9"},{"1":"/Digitalization","2":"/2019","3":"1"},{"1":"/Digitalization","2":"/2020","3":"4"},{"1":"/Machine","2":"/2017","3":"3"},{"1":"/Machine","2":"/2018","3":"4"},{"1":"/Machine","2":"/2019","3":"4"},{"1":"/Machine","2":"/2020","3":"10"},{"1":"/Machine Learning","2":"/2017","3":"2"},{"1":"/Product","2":"/2019","3":"3"},{"1":"/Program","2":"/2017","3":"1"},{"1":"/Program","2":"/2018","3":"3"},{"1":"/Program","2":"/2020","3":"2"},{"1":"/Software","2":"/2017","3":"4"},{"1":"/Software","2":"/2018","3":"14"},{"1":"/Software","2":"/2019","3":"2"},{"1":"/Software","2":"/2020","3":"14"},{"1":"/Solution","2":"/2019","3":"1"},{"1":"/System","2":"/2018","3":"11"},{"1":"/System","2":"/2019","3":"32"},{"1":"/System","2":"/2020","3":"25"},{"1":"/Technology","2":"/2018","3":"7"},{"1":"/Technology","2":"/2019","3":"10"},{"1":"/Technology","2":"/2020","3":"6"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(year_synonyms, aes(fill=Year, y=Count, x=Synonyms)) + 
    geom_bar(position="dodge", stat="identity", color = "black") +
    labs(x = "Tags") +
    theme(axis.text.x=element_text(angle=90,hjust=1))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->

## personal impression and percentage of synonyms

``` r
# combine personal impression and synonym data
impression_synonyms <- rbind(personal_impression_data, synonym_data)
impression_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"},{"1":"/Algorithm","2":"48","3":"9","4":"2","5":"1","6":"NA","7":"9","8":"NA","9":"6","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"1","18":"NA","19":"4","20":"NA","21":"NA","22":"1","23":"NA","24":"7","25":"NA","26":"8","_rn_":"5"},{"1":"/Application","2":"11","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"NA","9":"NA","10":"2","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"NA","24":"4","25":"NA","26":"NA","_rn_":"6"},{"1":"/Big Data","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"2","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"7"},{"1":"/Brain","2":"3","3":"NA","4":"NA","5":"3","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"8"},{"1":"/Chatbot","2":"18","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"2","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"16","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"9"},{"1":"/Cloud","2":"3","3":"NA","4":"NA","5":"2","6":"NA","7":"1","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"10"},{"1":"/Computer","2":"69","3":"NA","4":"8","5":"NA","6":"NA","7":"10","8":"3","9":"3","10":"NA","11":"1","12":"3","13":"1","14":"3","15":"NA","16":"NA","17":"9","18":"NA","19":"6","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"1","26":"19","_rn_":"12"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"1","10":"NA","11":"1","12":"2","13":"1","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"2","23":"2","24":"2","25":"1","26":"NA","_rn_":"13"},{"1":"/Digitalization","2":"5","3":"NA","4":"NA","5":"NA","6":"NA","7":"3","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"14"},{"1":"/Machine","2":"21","3":"NA","4":"1","5":"6","6":"NA","7":"NA","8":"1","9":"1","10":"NA","11":"NA","12":"2","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"2","22":"1","23":"NA","24":"3","25":"2","26":"NA","_rn_":"16"},{"1":"/Machine Learning","2":"2","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"17"},{"1":"/Product","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"3","25":"NA","26":"NA","_rn_":"18"},{"1":"/Program","2":"6","3":"NA","4":"NA","5":"NA","6":"1","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"3","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"19"},{"1":"/Software","2":"34","3":"NA","4":"NA","5":"1","6":"NA","7":"NA","8":"8","9":"NA","10":"NA","11":"NA","12":"14","13":"2","14":"NA","15":"1","16":"NA","17":"NA","18":"NA","19":"4","20":"NA","21":"3","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"21"},{"1":"/Solution","2":"1","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"1","25":"NA","26":"NA","_rn_":"22"},{"1":"/System","2":"68","3":"NA","4":"6","5":"NA","6":"NA","7":"2","8":"2","9":"5","10":"NA","11":"1","12":"2","13":"13","14":"NA","15":"NA","16":"1","17":"11","18":"NA","19":"NA","20":"NA","21":"2","22":"9","23":"6","24":"3","25":"NA","26":"5","_rn_":"23"},{"1":"/Technology","2":"23","3":"NA","4":"1","5":"3","6":"NA","7":"NA","8":"1","9":"NA","10":"2","11":"1","12":"NA","13":"1","14":"3","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"4","23":"NA","24":"3","25":"NA","26":"2","_rn_":"24"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
impression_synonyms <- impression_synonyms %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
impression_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/positive","2":"13","3":"2","4":"1"},{"1":"/positive","2":"13","3":"6","4":"1"},{"1":"/positive","2":"13","3":"8","4":"1"},{"1":"/positive","2":"13","3":"11","4":"1"},{"1":"/positive","2":"13","3":"12","4":"1"},{"1":"/positive","2":"13","3":"13","4":"1"},{"1":"/positive","2":"13","3":"14","4":"1"},{"1":"/positive","2":"13","3":"15","4":"1"},{"1":"/positive","2":"13","3":"16","4":"1"},{"1":"/positive","2":"13","3":"17","4":"1"},{"1":"/positive","2":"13","3":"19","4":"1"},{"1":"/positive","2":"13","3":"20","4":"1"},{"1":"/positive","2":"13","3":"23","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"3","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"4","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"5","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"7","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"9","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"18","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"21","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"22","4":"1"},{"1":"/negative","2":"3","3":"1","4":"1"},{"1":"/negative","2":"3","3":"10","4":"1"},{"1":"/negative","2":"3","3":"24","4":"1"},{"1":"/Algorithm","2":"48","3":"1","4":"9"},{"1":"/Algorithm","2":"48","3":"2","4":"2"},{"1":"/Algorithm","2":"48","3":"3","4":"1"},{"1":"/Algorithm","2":"48","3":"5","4":"9"},{"1":"/Algorithm","2":"48","3":"7","4":"6"},{"1":"/Algorithm","2":"48","3":"15","4":"1"},{"1":"/Algorithm","2":"48","3":"17","4":"4"},{"1":"/Algorithm","2":"48","3":"20","4":"1"},{"1":"/Algorithm","2":"48","3":"22","4":"7"},{"1":"/Algorithm","2":"48","3":"24","4":"8"},{"1":"/Application","2":"11","3":"3","4":"1"},{"1":"/Application","2":"11","3":"8","4":"2"},{"1":"/Application","2":"11","3":"14","4":"1"},{"1":"/Application","2":"11","3":"18","4":"1"},{"1":"/Application","2":"11","3":"20","4":"2"},{"1":"/Application","2":"11","3":"22","4":"4"},{"1":"/Big Data","2":"5","3":"5","4":"2"},{"1":"/Big Data","2":"5","3":"12","4":"1"},{"1":"/Big Data","2":"5","3":"20","4":"2"},{"1":"/Brain","2":"3","3":"3","4":"3"},{"1":"/Chatbot","2":"18","3":"12","4":"2"},{"1":"/Chatbot","2":"18","3":"20","4":"16"},{"1":"/Cloud","2":"3","3":"3","4":"2"},{"1":"/Cloud","2":"3","3":"5","4":"1"},{"1":"/Computer","2":"69","3":"2","4":"8"},{"1":"/Computer","2":"69","3":"5","4":"10"},{"1":"/Computer","2":"69","3":"6","4":"3"},{"1":"/Computer","2":"69","3":"7","4":"3"},{"1":"/Computer","2":"69","3":"9","4":"1"},{"1":"/Computer","2":"69","3":"10","4":"3"},{"1":"/Computer","2":"69","3":"11","4":"1"},{"1":"/Computer","2":"69","3":"12","4":"3"},{"1":"/Computer","2":"69","3":"15","4":"9"},{"1":"/Computer","2":"69","3":"17","4":"6"},{"1":"/Computer","2":"69","3":"21","4":"1"},{"1":"/Computer","2":"69","3":"22","4":"1"},{"1":"/Computer","2":"69","3":"23","4":"1"},{"1":"/Computer","2":"69","3":"24","4":"19"},{"1":"/Deep Learning / Networks","2":"20","3":"1","4":"7"},{"1":"/Deep Learning / Networks","2":"20","3":"7","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"9","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"10","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"11","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"18","4":"1"},{"1":"/Deep Learning / Networks","2":"20","3":"20","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"21","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"22","4":"2"},{"1":"/Deep Learning / Networks","2":"20","3":"23","4":"1"},{"1":"/Digitalization","2":"5","3":"5","4":"3"},{"1":"/Digitalization","2":"5","3":"6","4":"1"},{"1":"/Digitalization","2":"5","3":"8","4":"1"},{"1":"/Machine","2":"21","3":"2","4":"1"},{"1":"/Machine","2":"21","3":"3","4":"6"},{"1":"/Machine","2":"21","3":"6","4":"1"},{"1":"/Machine","2":"21","3":"7","4":"1"},{"1":"/Machine","2":"21","3":"10","4":"2"},{"1":"/Machine","2":"21","3":"12","4":"1"},{"1":"/Machine","2":"21","3":"17","4":"1"},{"1":"/Machine","2":"21","3":"19","4":"2"},{"1":"/Machine","2":"21","3":"20","4":"1"},{"1":"/Machine","2":"21","3":"22","4":"3"},{"1":"/Machine","2":"21","3":"23","4":"2"},{"1":"/Machine Learning","2":"2","3":"18","4":"1"},{"1":"/Machine Learning","2":"2","3":"23","4":"1"},{"1":"/Product","2":"3","3":"22","4":"3"},{"1":"/Program","2":"6","3":"4","4":"1"},{"1":"/Program","2":"6","3":"10","4":"3"},{"1":"/Program","2":"6","3":"17","4":"1"},{"1":"/Program","2":"6","3":"19","4":"1"},{"1":"/Software","2":"34","3":"3","4":"1"},{"1":"/Software","2":"34","3":"6","4":"8"},{"1":"/Software","2":"34","3":"10","4":"14"},{"1":"/Software","2":"34","3":"11","4":"2"},{"1":"/Software","2":"34","3":"13","4":"1"},{"1":"/Software","2":"34","3":"17","4":"4"},{"1":"/Software","2":"34","3":"19","4":"3"},{"1":"/Software","2":"34","3":"22","4":"1"},{"1":"/Solution","2":"1","3":"22","4":"1"},{"1":"/System","2":"68","3":"2","4":"6"},{"1":"/System","2":"68","3":"5","4":"2"},{"1":"/System","2":"68","3":"6","4":"2"},{"1":"/System","2":"68","3":"7","4":"5"},{"1":"/System","2":"68","3":"9","4":"1"},{"1":"/System","2":"68","3":"10","4":"2"},{"1":"/System","2":"68","3":"11","4":"13"},{"1":"/System","2":"68","3":"14","4":"1"},{"1":"/System","2":"68","3":"15","4":"11"},{"1":"/System","2":"68","3":"19","4":"2"},{"1":"/System","2":"68","3":"20","4":"9"},{"1":"/System","2":"68","3":"21","4":"6"},{"1":"/System","2":"68","3":"22","4":"3"},{"1":"/System","2":"68","3":"24","4":"5"},{"1":"/Technology","2":"23","3":"2","4":"1"},{"1":"/Technology","2":"23","3":"3","4":"3"},{"1":"/Technology","2":"23","3":"6","4":"1"},{"1":"/Technology","2":"23","3":"8","4":"2"},{"1":"/Technology","2":"23","3":"9","4":"1"},{"1":"/Technology","2":"23","3":"11","4":"1"},{"1":"/Technology","2":"23","3":"12","4":"3"},{"1":"/Technology","2":"23","3":"15","4":"1"},{"1":"/Technology","2":"23","3":"19","4":"1"},{"1":"/Technology","2":"23","3":"20","4":"4"},{"1":"/Technology","2":"23","3":"22","4":"3"},{"1":"/Technology","2":"23","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
impr <- impression_synonyms[c(1:24),]
syn <- impression_synonyms[25:128,]

# merge data based on the articles
impression_synonyms<- merge.data.frame(impr[-2],syn[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Personal_Impression" = 1, "Synonyms" = 2, "Count" = 3)
impression_synonyms
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Personal_Impression"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Synonyms"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/negative","2":"/Algorithm","3":"17"},{"1":"/negative","2":"/Computer","3":"22"},{"1":"/negative","2":"/Deep Learning / Networks","3":"9"},{"1":"/negative","2":"/Machine","3":"2"},{"1":"/negative","2":"/Program","3":"3"},{"1":"/negative","2":"/Software","3":"14"},{"1":"/negative","2":"/System","3":"7"},{"1":"/negative","2":"/Technology","3":"2"},{"1":"/neither positive nor negative","2":"/Algorithm","3":"23"},{"1":"/neither positive nor negative","2":"/Application","3":"6"},{"1":"/neither positive nor negative","2":"/Big Data","3":"2"},{"1":"/neither positive nor negative","2":"/Brain","3":"3"},{"1":"/neither positive nor negative","2":"/Cloud","3":"3"},{"1":"/neither positive nor negative","2":"/Computer","3":"16"},{"1":"/neither positive nor negative","2":"/Deep Learning / Networks","3":"7"},{"1":"/neither positive nor negative","2":"/Digitalization","3":"3"},{"1":"/neither positive nor negative","2":"/Machine","3":"10"},{"1":"/neither positive nor negative","2":"/Machine Learning","3":"1"},{"1":"/neither positive nor negative","2":"/Product","3":"3"},{"1":"/neither positive nor negative","2":"/Program","3":"1"},{"1":"/neither positive nor negative","2":"/Software","3":"2"},{"1":"/neither positive nor negative","2":"/Solution","3":"1"},{"1":"/neither positive nor negative","2":"/System","3":"17"},{"1":"/neither positive nor negative","2":"/Technology","3":"7"},{"1":"/positive","2":"/Algorithm","3":"8"},{"1":"/positive","2":"/Application","3":"5"},{"1":"/positive","2":"/Big Data","3":"3"},{"1":"/positive","2":"/Chatbot","3":"18"},{"1":"/positive","2":"/Computer","3":"31"},{"1":"/positive","2":"/Deep Learning / Networks","3":"4"},{"1":"/positive","2":"/Digitalization","3":"2"},{"1":"/positive","2":"/Machine","3":"9"},{"1":"/positive","2":"/Machine Learning","3":"1"},{"1":"/positive","2":"/Program","3":"2"},{"1":"/positive","2":"/Software","3":"18"},{"1":"/positive","2":"/System","3":"44"},{"1":"/positive","2":"/Technology","3":"14"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(impression_synonyms, aes(fill=Synonyms, y=Count, x=factor(Personal_Impression,levels=c("/positive","/neither positive nor negative","/negative")))) + 
    geom_bar(position="fill", stat="identity", color = "black") +
    labs(title = "",
         y = "Percentage",
         x = "Personal Impression")
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->

# illnesses

## illnesses total

``` r
ggplot(illness_data, aes(fill=Tags, y=Total, x=Tags)) + 
    geom_bar(position="dodge", stat="identity") +
    labs(y = "Count", x = "Tags") +
    theme(legend.position = "none") +
    scale_fill_manual(values=c("firebrick3","aquamarine4","mediumorchid4"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

## year and percentage of illnesses

``` r
# combine year and illness data
year_illness <- rbind(year_data, illness_data)
year_illness
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"1","20":"1","21":"NA","22":"NA","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"1"},{"1":"/2018","2":"4","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"1","15":"NA","16":"NA","17":"NA","18":"1","19":"NA","20":"NA","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"2"},{"1":"/2019","2":"8","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"1","11":"1","12":"NA","13":"NA","14":"NA","15":"1","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"1","_rn_":"3"},{"1":"/2020","2":"9","3":"1","4":"NA","5":"1","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"NA","12":"NA","13":"1","14":"NA","15":"NA","16":"1","17":"NA","18":"NA","19":"NA","20":"NA","21":"1","22":"NA","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"4"},{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1","_rn_":"25"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1","_rn_":"31"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"35"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
year_illness <- year_illness %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
year_illness
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/2017","2":"3","3":"17","4":"1"},{"1":"/2017","2":"3","3":"18","4":"1"},{"1":"/2017","2":"3","3":"23","4":"1"},{"1":"/2018","2":"4","3":"10","4":"1"},{"1":"/2018","2":"4","3":"12","4":"1"},{"1":"/2018","2":"4","3":"16","4":"1"},{"1":"/2018","2":"4","3":"20","4":"1"},{"1":"/2019","2":"8","3":"2","4":"1"},{"1":"/2019","2":"8","3":"8","4":"1"},{"1":"/2019","2":"8","3":"9","4":"1"},{"1":"/2019","2":"8","3":"13","4":"1"},{"1":"/2019","2":"8","3":"15","4":"1"},{"1":"/2019","2":"8","3":"21","4":"1"},{"1":"/2019","2":"8","3":"22","4":"1"},{"1":"/2019","2":"8","3":"24","4":"1"},{"1":"/2020","2":"9","3":"1","4":"1"},{"1":"/2020","2":"9","3":"3","4":"1"},{"1":"/2020","2":"9","3":"4","4":"1"},{"1":"/2020","2":"9","3":"5","4":"1"},{"1":"/2020","2":"9","3":"6","4":"1"},{"1":"/2020","2":"9","3":"7","4":"1"},{"1":"/2020","2":"9","3":"11","4":"1"},{"1":"/2020","2":"9","3":"14","4":"1"},{"1":"/2020","2":"9","3":"19","4":"1"},{"1":"/cancer","2":"38","3":"1","4":"2"},{"1":"/cancer","2":"38","3":"2","4":"2"},{"1":"/cancer","2":"38","3":"5","4":"4"},{"1":"/cancer","2":"38","3":"6","4":"1"},{"1":"/cancer","2":"38","3":"7","4":"2"},{"1":"/cancer","2":"38","3":"9","4":"1"},{"1":"/cancer","2":"38","3":"10","4":"2"},{"1":"/cancer","2":"38","3":"11","4":"4"},{"1":"/cancer","2":"38","3":"12","4":"2"},{"1":"/cancer","2":"38","3":"14","4":"1"},{"1":"/cancer","2":"38","3":"15","4":"6"},{"1":"/cancer","2":"38","3":"16","4":"1"},{"1":"/cancer","2":"38","3":"17","4":"4"},{"1":"/cancer","2":"38","3":"19","4":"1"},{"1":"/cancer","2":"38","3":"21","4":"1"},{"1":"/cancer","2":"38","3":"22","4":"2"},{"1":"/cancer","2":"38","3":"23","4":"1"},{"1":"/cancer","2":"38","3":"24","4":"1"},{"1":"/non-cancer","2":"23","3":"1","4":"1"},{"1":"/non-cancer","2":"23","3":"4","4":"1"},{"1":"/non-cancer","2":"23","3":"5","4":"1"},{"1":"/non-cancer","2":"23","3":"6","4":"1"},{"1":"/non-cancer","2":"23","3":"7","4":"1"},{"1":"/non-cancer","2":"23","3":"9","4":"3"},{"1":"/non-cancer","2":"23","3":"10","4":"1"},{"1":"/non-cancer","2":"23","3":"12","4":"4"},{"1":"/non-cancer","2":"23","3":"20","4":"1"},{"1":"/non-cancer","2":"23","3":"21","4":"1"},{"1":"/non-cancer","2":"23","3":"22","4":"4"},{"1":"/non-cancer","2":"23","3":"23","4":"3"},{"1":"/non-cancer","2":"23","3":"24","4":"1"},{"1":"/psychological","2":"7","3":"6","4":"1"},{"1":"/psychological","2":"7","3":"12","4":"1"},{"1":"/psychological","2":"7","3":"13","4":"1"},{"1":"/psychological","2":"7","3":"18","4":"3"},{"1":"/psychological","2":"7","3":"20","4":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
illn <- year_illness[25:60,]
year <- year_illness[1:24,]

# merge data based on the articles
year_illness <- merge.data.frame(illn[-2],year[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Illness" = 1, "Year" = 2, "Count" = 3)
year_illness
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Illness"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Year"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"/2017","3":"5"},{"1":"/cancer","2":"/2018","3":"5"},{"1":"/cancer","2":"/2019","3":"13"},{"1":"/cancer","2":"/2020","3":"15"},{"1":"/non-cancer","2":"/2017","3":"3"},{"1":"/non-cancer","2":"/2018","3":"6"},{"1":"/non-cancer","2":"/2019","3":"9"},{"1":"/non-cancer","2":"/2020","3":"5"},{"1":"/psychological","2":"/2017","3":"3"},{"1":"/psychological","2":"/2018","3":"2"},{"1":"/psychological","2":"/2019","3":"1"},{"1":"/psychological","2":"/2020","3":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(year_illness, aes(fill=Illness, y=Count, x=Year)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage") +
    scale_fill_manual(values=c("firebrick3","aquamarine4","mediumorchid4"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

## sentiment and illnesses

``` r
# combine illness and sentiment data
illness_sentiment <- rbind(illness_data, sentiment_data)
illness_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1","_rn_":"25"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1","_rn_":"31"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"35"},{"1":"/pro AI","2":"126","3":"NA","4":"7","5":"6","6":"NA","7":"4","8":"11","9":"4","10":"9","11":"1","12":"3","13":"10","14":"7","15":"2","16":"3","17":"7","18":"2","19":"4","20":"4","21":"7","22":"11","23":"4","24":"14","25":"2","26":"4","_rn_":"34"},{"1":"/neutral","2":"78","3":"1","4":"7","5":"1","6":"1","7":"2","8":"NA","9":"6","10":"3","11":"1","12":"4","13":"6","14":"3","15":"4","16":"5","17":"NA","18":"NA","19":"NA","20":"NA","21":"4","22":"13","23":"2","24":"10","25":"1","26":"4","_rn_":"30"},{"1":"/contra AI","2":"35","3":"3","4":"2","5":"NA","6":"NA","7":"2","8":"NA","9":"1","10":"1","11":"1","12":"3","13":"1","14":"1","15":"NA","16":"NA","17":"1","18":"NA","19":"NA","20":"NA","21":"1","22":"3","23":"NA","24":"3","25":"NA","26":"12","_rn_":"26"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
illness_sentiment <- illness_sentiment %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
illness_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"1","4":"2"},{"1":"/cancer","2":"38","3":"2","4":"2"},{"1":"/cancer","2":"38","3":"5","4":"4"},{"1":"/cancer","2":"38","3":"6","4":"1"},{"1":"/cancer","2":"38","3":"7","4":"2"},{"1":"/cancer","2":"38","3":"9","4":"1"},{"1":"/cancer","2":"38","3":"10","4":"2"},{"1":"/cancer","2":"38","3":"11","4":"4"},{"1":"/cancer","2":"38","3":"12","4":"2"},{"1":"/cancer","2":"38","3":"14","4":"1"},{"1":"/cancer","2":"38","3":"15","4":"6"},{"1":"/cancer","2":"38","3":"16","4":"1"},{"1":"/cancer","2":"38","3":"17","4":"4"},{"1":"/cancer","2":"38","3":"19","4":"1"},{"1":"/cancer","2":"38","3":"21","4":"1"},{"1":"/cancer","2":"38","3":"22","4":"2"},{"1":"/cancer","2":"38","3":"23","4":"1"},{"1":"/cancer","2":"38","3":"24","4":"1"},{"1":"/non-cancer","2":"23","3":"1","4":"1"},{"1":"/non-cancer","2":"23","3":"4","4":"1"},{"1":"/non-cancer","2":"23","3":"5","4":"1"},{"1":"/non-cancer","2":"23","3":"6","4":"1"},{"1":"/non-cancer","2":"23","3":"7","4":"1"},{"1":"/non-cancer","2":"23","3":"9","4":"3"},{"1":"/non-cancer","2":"23","3":"10","4":"1"},{"1":"/non-cancer","2":"23","3":"12","4":"4"},{"1":"/non-cancer","2":"23","3":"20","4":"1"},{"1":"/non-cancer","2":"23","3":"21","4":"1"},{"1":"/non-cancer","2":"23","3":"22","4":"4"},{"1":"/non-cancer","2":"23","3":"23","4":"3"},{"1":"/non-cancer","2":"23","3":"24","4":"1"},{"1":"/psychological","2":"7","3":"6","4":"1"},{"1":"/psychological","2":"7","3":"12","4":"1"},{"1":"/psychological","2":"7","3":"13","4":"1"},{"1":"/psychological","2":"7","3":"18","4":"3"},{"1":"/psychological","2":"7","3":"20","4":"1"},{"1":"/pro AI","2":"126","3":"2","4":"7"},{"1":"/pro AI","2":"126","3":"3","4":"6"},{"1":"/pro AI","2":"126","3":"5","4":"4"},{"1":"/pro AI","2":"126","3":"6","4":"11"},{"1":"/pro AI","2":"126","3":"7","4":"4"},{"1":"/pro AI","2":"126","3":"8","4":"9"},{"1":"/pro AI","2":"126","3":"9","4":"1"},{"1":"/pro AI","2":"126","3":"10","4":"3"},{"1":"/pro AI","2":"126","3":"11","4":"10"},{"1":"/pro AI","2":"126","3":"12","4":"7"},{"1":"/pro AI","2":"126","3":"13","4":"2"},{"1":"/pro AI","2":"126","3":"14","4":"3"},{"1":"/pro AI","2":"126","3":"15","4":"7"},{"1":"/pro AI","2":"126","3":"16","4":"2"},{"1":"/pro AI","2":"126","3":"17","4":"4"},{"1":"/pro AI","2":"126","3":"18","4":"4"},{"1":"/pro AI","2":"126","3":"19","4":"7"},{"1":"/pro AI","2":"126","3":"20","4":"11"},{"1":"/pro AI","2":"126","3":"21","4":"4"},{"1":"/pro AI","2":"126","3":"22","4":"14"},{"1":"/pro AI","2":"126","3":"23","4":"2"},{"1":"/pro AI","2":"126","3":"24","4":"4"},{"1":"/neutral","2":"78","3":"1","4":"1"},{"1":"/neutral","2":"78","3":"2","4":"7"},{"1":"/neutral","2":"78","3":"3","4":"1"},{"1":"/neutral","2":"78","3":"4","4":"1"},{"1":"/neutral","2":"78","3":"5","4":"2"},{"1":"/neutral","2":"78","3":"7","4":"6"},{"1":"/neutral","2":"78","3":"8","4":"3"},{"1":"/neutral","2":"78","3":"9","4":"1"},{"1":"/neutral","2":"78","3":"10","4":"4"},{"1":"/neutral","2":"78","3":"11","4":"6"},{"1":"/neutral","2":"78","3":"12","4":"3"},{"1":"/neutral","2":"78","3":"13","4":"4"},{"1":"/neutral","2":"78","3":"14","4":"5"},{"1":"/neutral","2":"78","3":"19","4":"4"},{"1":"/neutral","2":"78","3":"20","4":"13"},{"1":"/neutral","2":"78","3":"21","4":"2"},{"1":"/neutral","2":"78","3":"22","4":"10"},{"1":"/neutral","2":"78","3":"23","4":"1"},{"1":"/neutral","2":"78","3":"24","4":"4"},{"1":"/contra AI","2":"35","3":"1","4":"3"},{"1":"/contra AI","2":"35","3":"2","4":"2"},{"1":"/contra AI","2":"35","3":"5","4":"2"},{"1":"/contra AI","2":"35","3":"7","4":"1"},{"1":"/contra AI","2":"35","3":"8","4":"1"},{"1":"/contra AI","2":"35","3":"9","4":"1"},{"1":"/contra AI","2":"35","3":"10","4":"3"},{"1":"/contra AI","2":"35","3":"11","4":"1"},{"1":"/contra AI","2":"35","3":"12","4":"1"},{"1":"/contra AI","2":"35","3":"15","4":"1"},{"1":"/contra AI","2":"35","3":"19","4":"1"},{"1":"/contra AI","2":"35","3":"20","4":"3"},{"1":"/contra AI","2":"35","3":"22","4":"3"},{"1":"/contra AI","2":"35","3":"24","4":"12"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
illn <- illness_sentiment[1:36,]
sentim <- illness_sentiment[37:91,]

# merge data based on the articles
illness_sentiment <- merge.data.frame(illn[-2],sentim[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Illness" = 1, "Sentiment" = 2, "Count" = 3)
illness_sentiment
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Illness"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Sentiment"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"/contra AI","3":"31"},{"1":"/cancer","2":"/neutral","3":"56"},{"1":"/cancer","2":"/pro AI","3":"94"},{"1":"/non-cancer","2":"/contra AI","3":"29"},{"1":"/non-cancer","2":"/neutral","3":"48"},{"1":"/non-cancer","2":"/pro AI","3":"65"},{"1":"/psychological","2":"/contra AI","3":"4"},{"1":"/psychological","2":"/neutral","3":"20"},{"1":"/psychological","2":"/pro AI","3":"35"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(illness_sentiment, aes(fill=factor(Sentiment,levels=c("/pro AI","/neutral","/contra AI")), y=Count, x=Illness)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "Sentiment") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

## personal impression and illnesses

``` r
# combine illness and personal impression data
illness_impression <- rbind(illness_data, personal_impression_data)
illness_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1","_rn_":"25"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1","_rn_":"31"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"35"},{"1":"/positive","2":"13","3":"NA","4":"1","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"1","11":"NA","12":"NA","13":"1","14":"1","15":"1","16":"1","17":"1","18":"1","19":"1","20":"NA","21":"1","22":"1","23":"NA","24":"NA","25":"1","26":"NA","_rn_":"33"},{"1":"/neither positive nor negative","2":"8","3":"NA","4":"NA","5":"1","6":"1","7":"1","8":"NA","9":"1","10":"NA","11":"1","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"1","21":"NA","22":"NA","23":"1","24":"1","25":"NA","26":"NA","_rn_":"29"},{"1":"/negative","2":"3","3":"1","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"1","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA","25":"NA","26":"1","_rn_":"28"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
illness_impression <- illness_impression %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
illness_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"1","4":"2"},{"1":"/cancer","2":"38","3":"2","4":"2"},{"1":"/cancer","2":"38","3":"5","4":"4"},{"1":"/cancer","2":"38","3":"6","4":"1"},{"1":"/cancer","2":"38","3":"7","4":"2"},{"1":"/cancer","2":"38","3":"9","4":"1"},{"1":"/cancer","2":"38","3":"10","4":"2"},{"1":"/cancer","2":"38","3":"11","4":"4"},{"1":"/cancer","2":"38","3":"12","4":"2"},{"1":"/cancer","2":"38","3":"14","4":"1"},{"1":"/cancer","2":"38","3":"15","4":"6"},{"1":"/cancer","2":"38","3":"16","4":"1"},{"1":"/cancer","2":"38","3":"17","4":"4"},{"1":"/cancer","2":"38","3":"19","4":"1"},{"1":"/cancer","2":"38","3":"21","4":"1"},{"1":"/cancer","2":"38","3":"22","4":"2"},{"1":"/cancer","2":"38","3":"23","4":"1"},{"1":"/cancer","2":"38","3":"24","4":"1"},{"1":"/non-cancer","2":"23","3":"1","4":"1"},{"1":"/non-cancer","2":"23","3":"4","4":"1"},{"1":"/non-cancer","2":"23","3":"5","4":"1"},{"1":"/non-cancer","2":"23","3":"6","4":"1"},{"1":"/non-cancer","2":"23","3":"7","4":"1"},{"1":"/non-cancer","2":"23","3":"9","4":"3"},{"1":"/non-cancer","2":"23","3":"10","4":"1"},{"1":"/non-cancer","2":"23","3":"12","4":"4"},{"1":"/non-cancer","2":"23","3":"20","4":"1"},{"1":"/non-cancer","2":"23","3":"21","4":"1"},{"1":"/non-cancer","2":"23","3":"22","4":"4"},{"1":"/non-cancer","2":"23","3":"23","4":"3"},{"1":"/non-cancer","2":"23","3":"24","4":"1"},{"1":"/psychological","2":"7","3":"6","4":"1"},{"1":"/psychological","2":"7","3":"12","4":"1"},{"1":"/psychological","2":"7","3":"13","4":"1"},{"1":"/psychological","2":"7","3":"18","4":"3"},{"1":"/psychological","2":"7","3":"20","4":"1"},{"1":"/positive","2":"13","3":"2","4":"1"},{"1":"/positive","2":"13","3":"6","4":"1"},{"1":"/positive","2":"13","3":"8","4":"1"},{"1":"/positive","2":"13","3":"11","4":"1"},{"1":"/positive","2":"13","3":"12","4":"1"},{"1":"/positive","2":"13","3":"13","4":"1"},{"1":"/positive","2":"13","3":"14","4":"1"},{"1":"/positive","2":"13","3":"15","4":"1"},{"1":"/positive","2":"13","3":"16","4":"1"},{"1":"/positive","2":"13","3":"17","4":"1"},{"1":"/positive","2":"13","3":"19","4":"1"},{"1":"/positive","2":"13","3":"20","4":"1"},{"1":"/positive","2":"13","3":"23","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"3","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"4","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"5","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"7","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"9","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"18","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"21","4":"1"},{"1":"/neither positive nor negative","2":"8","3":"22","4":"1"},{"1":"/negative","2":"3","3":"1","4":"1"},{"1":"/negative","2":"3","3":"10","4":"1"},{"1":"/negative","2":"3","3":"24","4":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
illn <- illness_impression[1:36,]
impr <- illness_impression[37:60,]

# merge data based on the articles
illness_impression <- merge.data.frame(illn[-2],impr[-2],by="article") %>% 
                            select(c(2,3,4)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Illness" = 1, "Impression" = 2, "Count" = 3)
illness_impression
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Illness"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Impression"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"/negative","3":"5"},{"1":"/cancer","2":"/neither positive nor negative","3":"10"},{"1":"/cancer","2":"/positive","3":"23"},{"1":"/non-cancer","2":"/negative","3":"3"},{"1":"/non-cancer","2":"/neither positive nor negative","3":"11"},{"1":"/non-cancer","2":"/positive","3":"9"},{"1":"/psychological","2":"/neither positive nor negative","3":"3"},{"1":"/psychological","2":"/positive","3":"4"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(illness_impression, aes(fill=factor(Impression,levels=c("/positive","/neither positive nor negative","/negative")), y=Count, x=Illness)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "Personal Impression") +
    scale_fill_manual(values=c("palegreen3","seashell3","lightcoral"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

## SWOT and illnesses

``` r
# combine illness and SWOT data
illness_SWOT <- rbind(illness_data, SWOT_data)
illness_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["1"],"name":[3],"type":["int"],"align":["right"]},{"label":["2"],"name":[4],"type":["int"],"align":["right"]},{"label":["3"],"name":[5],"type":["int"],"align":["right"]},{"label":["4"],"name":[6],"type":["int"],"align":["right"]},{"label":["5"],"name":[7],"type":["int"],"align":["right"]},{"label":["6"],"name":[8],"type":["int"],"align":["right"]},{"label":["7"],"name":[9],"type":["int"],"align":["right"]},{"label":["8"],"name":[10],"type":["int"],"align":["right"]},{"label":["9"],"name":[11],"type":["int"],"align":["right"]},{"label":["10"],"name":[12],"type":["int"],"align":["right"]},{"label":["11"],"name":[13],"type":["int"],"align":["right"]},{"label":["12"],"name":[14],"type":["int"],"align":["right"]},{"label":["13"],"name":[15],"type":["int"],"align":["right"]},{"label":["14"],"name":[16],"type":["int"],"align":["right"]},{"label":["15"],"name":[17],"type":["int"],"align":["right"]},{"label":["16"],"name":[18],"type":["int"],"align":["right"]},{"label":["17"],"name":[19],"type":["int"],"align":["right"]},{"label":["18"],"name":[20],"type":["int"],"align":["right"]},{"label":["19"],"name":[21],"type":["int"],"align":["right"]},{"label":["20"],"name":[22],"type":["int"],"align":["right"]},{"label":["21"],"name":[23],"type":["int"],"align":["right"]},{"label":["22"],"name":[24],"type":["int"],"align":["right"]},{"label":["23"],"name":[25],"type":["int"],"align":["right"]},{"label":["24"],"name":[26],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"2","4":"2","5":"NA","6":"NA","7":"4","8":"1","9":"2","10":"NA","11":"1","12":"2","13":"4","14":"2","15":"NA","16":"1","17":"6","18":"1","19":"4","20":"NA","21":"1","22":"NA","23":"1","24":"2","25":"1","26":"1","_rn_":"25"},{"1":"/non-cancer","2":"23","3":"1","4":"NA","5":"NA","6":"1","7":"1","8":"1","9":"1","10":"NA","11":"3","12":"1","13":"NA","14":"4","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"1","23":"1","24":"4","25":"3","26":"1","_rn_":"31"},{"1":"/psychological","2":"7","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"1","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"1","15":"1","16":"NA","17":"NA","18":"NA","19":"NA","20":"3","21":"NA","22":"1","23":"NA","24":"NA","25":"NA","26":"NA","_rn_":"35"},{"1":"/strength","2":"59","3":"NA","4":"1","5":"2","6":"NA","7":"2","8":"4","9":"3","10":"3","11":"2","12":"1","13":"4","14":"8","15":"NA","16":"1","17":"2","18":"3","19":"3","20":"NA","21":"2","22":"1","23":"2","24":"10","25":"3","26":"2","_rn_":"39"},{"1":"/weakness","2":"60","3":"2","4":"5","5":"1","6":"1","7":"3","8":"NA","9":"6","10":"2","11":"1","12":"3","13":"4","14":"NA","15":"NA","16":"2","17":"5","18":"NA","19":"NA","20":"NA","21":"5","22":"2","23":"2","24":"4","25":"2","26":"10","_rn_":"44"},{"1":"/opportunity","2":"112","3":"NA","4":"2","5":"6","6":"1","7":"7","8":"2","9":"5","10":"6","11":"2","12":"3","13":"6","14":"7","15":"2","16":"6","17":"8","18":"NA","19":"3","20":"2","21":"9","22":"10","23":"9","24":"14","25":"1","26":"1","_rn_":"32"},{"1":"/threat","2":"26","3":"1","4":"1","5":"3","6":"NA","7":"5","8":"NA","9":"NA","10":"3","11":"NA","12":"1","13":"1","14":"NA","15":"NA","16":"2","17":"2","18":"NA","19":"NA","20":"NA","21":"NA","22":"2","23":"NA","24":"2","25":"1","26":"2","_rn_":"40"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
# summarize articles and counts
illness_SWOT <- illness_SWOT %>%
  pivot_longer(3:26, names_to = "article", values_to = "count") %>% 
  drop_na()
illness_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Tags"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Total"],"name":[2],"type":["int"],"align":["right"]},{"label":["article"],"name":[3],"type":["chr"],"align":["left"]},{"label":["count"],"name":[4],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"38","3":"1","4":"2"},{"1":"/cancer","2":"38","3":"2","4":"2"},{"1":"/cancer","2":"38","3":"5","4":"4"},{"1":"/cancer","2":"38","3":"6","4":"1"},{"1":"/cancer","2":"38","3":"7","4":"2"},{"1":"/cancer","2":"38","3":"9","4":"1"},{"1":"/cancer","2":"38","3":"10","4":"2"},{"1":"/cancer","2":"38","3":"11","4":"4"},{"1":"/cancer","2":"38","3":"12","4":"2"},{"1":"/cancer","2":"38","3":"14","4":"1"},{"1":"/cancer","2":"38","3":"15","4":"6"},{"1":"/cancer","2":"38","3":"16","4":"1"},{"1":"/cancer","2":"38","3":"17","4":"4"},{"1":"/cancer","2":"38","3":"19","4":"1"},{"1":"/cancer","2":"38","3":"21","4":"1"},{"1":"/cancer","2":"38","3":"22","4":"2"},{"1":"/cancer","2":"38","3":"23","4":"1"},{"1":"/cancer","2":"38","3":"24","4":"1"},{"1":"/non-cancer","2":"23","3":"1","4":"1"},{"1":"/non-cancer","2":"23","3":"4","4":"1"},{"1":"/non-cancer","2":"23","3":"5","4":"1"},{"1":"/non-cancer","2":"23","3":"6","4":"1"},{"1":"/non-cancer","2":"23","3":"7","4":"1"},{"1":"/non-cancer","2":"23","3":"9","4":"3"},{"1":"/non-cancer","2":"23","3":"10","4":"1"},{"1":"/non-cancer","2":"23","3":"12","4":"4"},{"1":"/non-cancer","2":"23","3":"20","4":"1"},{"1":"/non-cancer","2":"23","3":"21","4":"1"},{"1":"/non-cancer","2":"23","3":"22","4":"4"},{"1":"/non-cancer","2":"23","3":"23","4":"3"},{"1":"/non-cancer","2":"23","3":"24","4":"1"},{"1":"/psychological","2":"7","3":"6","4":"1"},{"1":"/psychological","2":"7","3":"12","4":"1"},{"1":"/psychological","2":"7","3":"13","4":"1"},{"1":"/psychological","2":"7","3":"18","4":"3"},{"1":"/psychological","2":"7","3":"20","4":"1"},{"1":"/strength","2":"59","3":"2","4":"1"},{"1":"/strength","2":"59","3":"3","4":"2"},{"1":"/strength","2":"59","3":"5","4":"2"},{"1":"/strength","2":"59","3":"6","4":"4"},{"1":"/strength","2":"59","3":"7","4":"3"},{"1":"/strength","2":"59","3":"8","4":"3"},{"1":"/strength","2":"59","3":"9","4":"2"},{"1":"/strength","2":"59","3":"10","4":"1"},{"1":"/strength","2":"59","3":"11","4":"4"},{"1":"/strength","2":"59","3":"12","4":"8"},{"1":"/strength","2":"59","3":"14","4":"1"},{"1":"/strength","2":"59","3":"15","4":"2"},{"1":"/strength","2":"59","3":"16","4":"3"},{"1":"/strength","2":"59","3":"17","4":"3"},{"1":"/strength","2":"59","3":"19","4":"2"},{"1":"/strength","2":"59","3":"20","4":"1"},{"1":"/strength","2":"59","3":"21","4":"2"},{"1":"/strength","2":"59","3":"22","4":"10"},{"1":"/strength","2":"59","3":"23","4":"3"},{"1":"/strength","2":"59","3":"24","4":"2"},{"1":"/weakness","2":"60","3":"1","4":"2"},{"1":"/weakness","2":"60","3":"2","4":"5"},{"1":"/weakness","2":"60","3":"3","4":"1"},{"1":"/weakness","2":"60","3":"4","4":"1"},{"1":"/weakness","2":"60","3":"5","4":"3"},{"1":"/weakness","2":"60","3":"7","4":"6"},{"1":"/weakness","2":"60","3":"8","4":"2"},{"1":"/weakness","2":"60","3":"9","4":"1"},{"1":"/weakness","2":"60","3":"10","4":"3"},{"1":"/weakness","2":"60","3":"11","4":"4"},{"1":"/weakness","2":"60","3":"14","4":"2"},{"1":"/weakness","2":"60","3":"15","4":"5"},{"1":"/weakness","2":"60","3":"19","4":"5"},{"1":"/weakness","2":"60","3":"20","4":"2"},{"1":"/weakness","2":"60","3":"21","4":"2"},{"1":"/weakness","2":"60","3":"22","4":"4"},{"1":"/weakness","2":"60","3":"23","4":"2"},{"1":"/weakness","2":"60","3":"24","4":"10"},{"1":"/opportunity","2":"112","3":"2","4":"2"},{"1":"/opportunity","2":"112","3":"3","4":"6"},{"1":"/opportunity","2":"112","3":"4","4":"1"},{"1":"/opportunity","2":"112","3":"5","4":"7"},{"1":"/opportunity","2":"112","3":"6","4":"2"},{"1":"/opportunity","2":"112","3":"7","4":"5"},{"1":"/opportunity","2":"112","3":"8","4":"6"},{"1":"/opportunity","2":"112","3":"9","4":"2"},{"1":"/opportunity","2":"112","3":"10","4":"3"},{"1":"/opportunity","2":"112","3":"11","4":"6"},{"1":"/opportunity","2":"112","3":"12","4":"7"},{"1":"/opportunity","2":"112","3":"13","4":"2"},{"1":"/opportunity","2":"112","3":"14","4":"6"},{"1":"/opportunity","2":"112","3":"15","4":"8"},{"1":"/opportunity","2":"112","3":"17","4":"3"},{"1":"/opportunity","2":"112","3":"18","4":"2"},{"1":"/opportunity","2":"112","3":"19","4":"9"},{"1":"/opportunity","2":"112","3":"20","4":"10"},{"1":"/opportunity","2":"112","3":"21","4":"9"},{"1":"/opportunity","2":"112","3":"22","4":"14"},{"1":"/opportunity","2":"112","3":"23","4":"1"},{"1":"/opportunity","2":"112","3":"24","4":"1"},{"1":"/threat","2":"26","3":"1","4":"1"},{"1":"/threat","2":"26","3":"2","4":"1"},{"1":"/threat","2":"26","3":"3","4":"3"},{"1":"/threat","2":"26","3":"5","4":"5"},{"1":"/threat","2":"26","3":"8","4":"3"},{"1":"/threat","2":"26","3":"10","4":"1"},{"1":"/threat","2":"26","3":"11","4":"1"},{"1":"/threat","2":"26","3":"14","4":"2"},{"1":"/threat","2":"26","3":"15","4":"2"},{"1":"/threat","2":"26","3":"20","4":"2"},{"1":"/threat","2":"26","3":"22","4":"2"},{"1":"/threat","2":"26","3":"23","4":"1"},{"1":"/threat","2":"26","3":"24","4":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
illn <- illness_SWOT[1:36,]
swot <- illness_SWOT[37:109,]

# merge data based on the articles
illness_SWOT <- merge.data.frame(illn[-2],swot[-2],by="article") %>% 
                            select(c(2,4,5)) %>% 
                            group_by(Tags.x, Tags.y) %>%
                            summarise_each(list(sum = sum)) %>% 
                            rename("Illness" = 1, "SWOT" = 2, "Count" = 3)
illness_SWOT
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Illness"],"name":[1],"type":["chr"],"align":["left"]},{"label":["SWOT"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Count"],"name":[3],"type":["int"],"align":["right"]}],"data":[{"1":"/cancer","2":"/opportunity","3":"85"},{"1":"/cancer","2":"/strength","3":"53"},{"1":"/cancer","2":"/threat","3":"18"},{"1":"/cancer","2":"/weakness","3":"54"},{"1":"/non-cancer","2":"/opportunity","3":"62"},{"1":"/non-cancer","2":"/strength","3":"38"},{"1":"/non-cancer","2":"/threat","3":"14"},{"1":"/non-cancer","2":"/weakness","3":"36"},{"1":"/psychological","2":"/opportunity","3":"23"},{"1":"/psychological","2":"/strength","3":"13"},{"1":"/psychological","2":"/threat","3":"2"},{"1":"/psychological","2":"/weakness","3":"2"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
ggplot(illness_SWOT, aes(fill=factor(SWOT, levels=c("/strength","/weakness","/opportunity","/threat")), y=Count, x=Illness)) + 
    geom_bar(position="fill", stat="identity") +
    labs(y = "Percentage",
         fill = "SWOT") +
    scale_fill_manual(values=c("deeppink3","cadetblue2","coral1","red3"))
```

![](Analyses_and_Diagrams_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->
