# hse_hw3_chromhmm
Eighth homework of Bioinformatics course in HSE

[Google colab](https://colab.research.google.com/drive/1Krla4mi0iLQD6gXJbTCq0tjke86RVpAO?usp=sharing)

В прошлом домашнем задании моя клеточная линия была $MCF-7$, но в той таблице, что приведенав в задании у него только 5 различных модификаций гистонов, поэтому я возьму для анализа клеточную линию HepG2.

## Выбор образцов
Я взяла ровно 10, больше там вроде и нет:
H2AFZ

H3K27ac

H3K27me3

H3K36me3

H3K4me1

H3K4me2

H3K4me3

H3K79me2

H3K9ac

H4K20me1

И контрольный образец можно найти [тут](http://hgdownload.cse.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeBroadHistone/wgEncodeBroadHistoneHepg2ControlStdAlnRep1.bam)

## Графики ChromHMM

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/d8667f95-1bac-4e6f-96c8-32c253285e59)

[В этом источнике](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1489-y/figures/6) написано, что этот график показывает насколько типично будет какая-то метка для каждого состояния. 

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/d3d601f5-a87d-4ba3-bbde-bcdfb06e3a25)

В том же источнике, что и ранее, указано, что этот график отвечает за то, насколько верно, что что следующий отрезок будет лежать в одном из 10 состояниях (вообще видно, что прямая диагональна, то есть вероятность того, что следующий кусок будет другого состояния в отличия от данного очень мала)

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/a95fbae2-694b-44bb-af75-91fc55926f10)

Этот график представляет из себя общую статистику. И можно заметить, что состояние 2 встречается чаще всего. Приведу цитату из [источника](https://www.researchgate.net/figure/Sample-outputs-of-ChromHMM-a-Example-of-chromatin-state-annotation-tracks-produced_fig1_221869893) о том, что этот график обозначет: *The columns indicate the relative percentage of the genome represented by each chromatin state and relative fold enrichment for several types of annotation.*

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/1b00b0d1-ea1c-4f67-a684-3afc9d9b6863)

Здесь как раз показывается относительность для каждого состояния в TSS(transcription start site). Видим, что с TSS ассоциированны состояния 9 и 10. А также из прошлого графика видно, что эти же состояния ассоциироваеы с CpG островками, что может говорить о том, что эти состояния -- промотеры.

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/be7874c5-e934-4ed3-9f51-47f9382a145c)

Здесь как раз показывается относительность для каждого состояния в TES(transcript end site). Видим, что с TES ассоциированы с состояниями 3, 9 и 10

##  UCSC GenomeBrowser
Загрузила файл `HepG2_10_dense.bed`

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/cfd7d768-21b0-4a88-88ee-2183652e683d)

Получилось что-то такое:

![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/3be74422-fe55-4d4b-8070-12a90b01c969)

## Анализ полученных результатов

## Бонус
