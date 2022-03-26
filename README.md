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
      
      
