# hse_hw3_chromhmm
# Запуск ChromHMM
Цель задания состоит в том, что нужно разбить (аннотировать) геном человека на разные типы эпигенетических состояний с помощью программы ChromHMM.  
Для эксперимента я взяла клеточную линию DND-41 и 10 модификаций гистонов (но я взяла 8 модификаций гистонов и 2 транскрипционный фактора).   
Покажу в таблице соответствие файла и метки.  
|mark | file | full file |
|-----|-----|------------|
| H2az   | H2azAlnRep1.bam   | wgEncodeBroadHistoneDnd41H2azAlnRep1.bam |
| H3k27ac   | H3k27acAlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k27acAlnRep1.bam |
| H3k27me3   | H3k27me3AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k27me3AlnRep1.bam|
| H3k36me3   | H3k36me3AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k36me3AlnRep1.bam|
| H3k04me1   | H3k04me1AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k04me1AlnRep1.bam|
| H3k04me2   | H3k04me2AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k04me2AlnRep1.bam|
| H3k04me3   | H3k04me3AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k04me3AlnRep1.bam|
| H3k79me2   | H3k79me2AlnRep1.bam   | wgEncodeBroadHistoneDnd41H3k79me2AlnRep1.bam|
| H3k09me3   | H3k09me3AlnRep1.bam   |wgEncodeBroadHistoneDnd41H3k09me3AlnRep1.bam|
| H4k20me1   | H4k20me1AlnRep1.bam   |wgEncodeBroadHistoneDnd41H4k20me1AlnRep1.bam|
  
    
Также хочется показать содержимое [cellmarkfiletable.txt файла](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/cellmarkfiletable.txt), который нужен для запуска ChromHMM:  
  
  
  
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/picture_file.PNG)
  
  
# Анализ результатов
## Графики ChromHmm    
Посмотрим на выдачу ChromHmm и попробуем сделать некоторые гипотезы о состояниях.  
  
Для начала, мы можем узнать встречаемость наших меток на разных состояниях 1-10 (к сожалению, я написала в файле немного длинное название, но в целом понятно, что это и есть названия меток).  
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/LearnModelOutput/emissions_10.png) ![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/from_article.PNG)      
  
Например, можно предположить, что состояния 8 - 10 соответствуют началу тела гена.  
  
  
Кроме того, можем посмотреть на файл с общей статистикой по состояниям:  
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/LearnModelOutput/DND41_10_overlap.png)  
  
Здесь второе состояние (2) - наиболее встречаемое в геноме.  
Состояние 10 содержит много CpG островков, а значит, может соответствовать промоторам. Кроме того, состояние 10 ассоциировано с TSS (То есть явно можно проверять гипотезу, что состояние 10 - это начало транскрипции).    
Состояния 1,2,3 могут соответствовать репрессированному гетерохроматину (так как ассоциированы с lamina).    
      
## UCSC GenomeBrowser
Рассмотрим для начала ген TP73.    
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/tp73.PNG)    
Для него мы видим, что действительно состояние 10 соответствует переходу к TSS. Состояния 5 и 7 как-то связаны с расположением интронов, а состояние 4 - экзонов. 
Состояния 1 и 2 скорее соответствует межгенному пространству, чем какому-то определенному участку гена.  
  
Рассмотрим участок с геном EIF4G3.  
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/EIF4G3.PNG)    
Здесь мы наблюдаем, что состояние 10 ассоциировано с TES и модиикациями H3k4me1, H3k4me2, H3k4me3, H3k9ac, H3k27ac.  
Интересно, что состояние 9 всегда на этом участке ассоциирована с этими же метками и идет вслед за состоянием 10, а состояние 8 часто перед ними.  
Состояние 4 и 5 все так же, как мне кажется зависят от расположения экзонов и интронов соответственно (4 там, где скопление эконов).     
  
Попробуем посмотреть на достаточно широкий участок со множеством генов.    
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/wide_view.PNG)    
Видно, что состояния 1 и 2 (и 3, но их в принципе мало) часто соответствуют пространству с редкими генами. Кроме того, эти участки почти полностью исключают все другие состояния рядом (не перемешиваются), а значит в них скорее всего нет н участков энхансеров, промотеров и других, связанных с активной экспрессией. Значит, можно сделать вывод, что гипотеза про репресированный гетерозроматин для состояний 1, 2 и 3 подтверждается.     
Что касается участков 4, 5, 6 и 7, то можно предположить, что они разделены по принципу того, что какие-то гены имеют слабую экспресию, а какие-то сильную. Например, состоянию weak promoter, weak enhancer могут соответствовать состояния 4 и 5, а strong promoter или enhancer - состояния 6 и 7, так как часто идут в паре на участках.    
Мне кажется, чтобы решить этот вопрос (какие состояния отвечают за сильную экспресию, а какие за слабую), нужно посмотреть на то, как жспрессируются отдельные гены, которые мы уже рассмотрели выше.  
## Article
Я прочитала оригинальную статью [Ernst and Kellis, 2010](https://drive.google.com/file/d/1uftwCcvl1lW4sAVPvka0JFIr5A9kLbF6/view?usp=sharing) по аннотированию состояний и попробую сопоставить приведенные там рассуждения с данными, которые получила выше.  
Во-первых, можно сказать про большую группу состояний промотера. В статье сказано, что все состояния промотера могут соответствовать большому количеству CpG Islands, быть ассоциированы с гистоновой модификацией H3k4me3. Однако, они отличаются друг от друга силой экспрессии и модификациями H3K79me2/3, H4K20me1, H3K4me1/2 и H3K9me1. По отношению к региону TSS тоже нельзя однозначно сказать. Различные состояния могут находиться на различном расстоянии от старта транскрипции.   
Отсюда можно предположить, что состояние 10 является состоянием промотера. Я думаю, что состояния 8 и 9 тоже являются состояниями участка перед транскрипцией, так как ассоциированы с меткой H3k4me2 (состояние промотера согласно таблице в статье).    
Так как состоянияе 8 ассоциировано с H3k36me3 по графикам ChromHmm, то согласно таблице статьи это состояние - Transcribed promoter; highest expr.  
Во-вторых, мы можем обозначить Large-scaled repressed states. Такие состояния ассоциированы с метками H3K27me3 и H3K9me3. Что удивительно, как и состояния 1 и 2. Выше мы выдвинули гипотезу, что состояния 1,2 и 3 могут соответствовать репрессированному гетерохроматину, и по геномному браузеру мы увидели подтверждающие сегментации. Исходя из фактов статьи, можно сказать, что состояния 1 и 2 соответствуют repressed состоянию (репрессированному гетерохроматину). Насчет состояния 3 в статье я не нашла подстверждения. Судя по таблице з статьи, состояние 3 - это скорее Repetitive участок (Ассоциирован с H3k9me3).     
Получается, остается разобраться с состояниями 4, 5, 6 и 7.    
![](https://github.com/kseniashilova/hse_hw3_chromhmm/blob/main/pic/article_transcribed.PNG)    
На картинке из оригинальной статьи видно, что действительно участки на транскрибирующейся части можно разделить на группы. Состояния 20-26 (Transcribed 5′ distal; exons, spliced exons, strong enhancer in transcribed regions) из статьи соответствуют состояниям 4 и 6 (оба на участках с большим количеством экзонов и оба соответствуют метке H3k36me3). Что касается состояния 5, то скорее всего ему соответствуют состояния 17-19 из статьи (Transcribed less 5′ proximal, med expr), что подтверждают гистоновые модификации. 

Состояния 12-16 (Transcribed 5′ proximal, higher expr) из статьи похожи на состояние 7 из эксперимента в этом домашнем задании, это можно понять потому, что состояние 7 - это явно не промотер, по первому графику из выдачи ChromHmm, а метка H3k79me2 и большое количество интронов указывает на состояния 12-16.     

Приведу таблицу для сопоставления состояний и их аннотаций, основываясь на рассуждениях выше. В столбцах таблицы обозначим, доказывает ли источник предположение (ну или хотя бы не опровергает ли).    
| State | Name| Tables ChromHmm | Visualisation GenomeBrowser | Article |
|-------|-----|------------|-----------------------------|---------|
|  1    | Repressed heterochromatin | proved |proved | proved |
|  2    |  Repressed heterochromatin | proved |proved | proved |
|  3    |  Repetitive | proved | not enough information | proved |
|  4    |  Transcribed 5′ distal; exons| proved| proved| proved, but there are a lot of approproate states for "4" (strong enhancer in transcribed regions, spliced exons) |
|  5    |  Transcribed less 5′ proximal, med expr | proved | proved | proved |
|  6    |  Transcribed 5′ distal; exons| proved| proved| proved, but there are a lot of approproate states for "4" (strong enhancer in transcribed regions, spliced exons) |
|  7    | Transcribed 5′ proximal, higher expr | proved | proved | proved |
|  8    | Transcribed promoter; highest expr | proved | proved | proved |
|  9    |  Promoter | proved | proved | proved |
|  10    |  Promoter | proved | proved | proved |  
