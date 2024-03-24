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

| Состояние |	Название типа   |	Метки                                  | CpG островки | TSS                                        |	TES                             |	Lamina | Summary | Картинка |
|:---------:|:---------------:|:--------------------------------------:|:------------:|:------------------------------------------:|:--------------------------------:|:------:|:-------:|:--------:|
| 1         |	Heterochromatin | H3K27me3 H4K20me1  H2AFZ H3K4me1       | +-           | +- Очень слабо выражены на всем промежутке | +- Выражены на всем промежутке   | +      | В целом везде выражено слабо, кроме H3K27me3 -- ассоциация с гетерохроматическими областями, в геноме его относительно много | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/7792b1ec-10c9-4e8d-a8be-9c1a861bb602) |
| 2         |	Heterochromatin | Очень слабо в H3K27me3 H4K20me1  H2AFZ | -            | -                                          | +- На всем промежутке слабая выраженность | +       | Больше всего встречается в геноме, но сопряжен слабо со всеми метками, по браузеру я бы сказала, что больше всего сопряжен с H3K27me3 |  ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/57f31afe-6aeb-41ed-a991-4f92bb362c82)| 
| 3         | Transcribed     | H3K36me3 H3K79me2 H3K36me3             | -            | - Небольшая выраженность после             | + Выраженность есть на всем промежутке, ближе к его началу выраженность больше| +- | Есть ассоциации с SeqExon и с SeqGene, в геноме также относительно много, по браузеру ассоциация с H3K36me3, попадает на экзоны  | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/dbb23cba-1888-4fde-bb66-12a74262f318)|
| 4         | Transcribed     | H3K79me2 H3K36me3 H3K36me3 H3K4me1     | -            | -                                          | - Слабая выраженность, но до чуть больше выражено | - | Cильные сигналы для H3K79me2 - ассоциация с транскрибируемыми областями активных генов, сильная ассоциация с SeqGene | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/4ab2e89e-0d38-4998-bb56-df803b961ff5) |
| 5         | Transcribed     | Во всех, кроме H3K27me3 H2AFZ          | -            | - Выражен больше на границах               | +- Ярко выражен до, а после уже не очень | - | Редко встречается в геноме, сильные сигналы для H3K4me1 и H3K79me2 - ассоциация с транскрибируемыми областями активных генов, сильная ассоциация с SeqGene и средняя с SeqExon | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/e97ed084-2c3b-45ae-847c-97e00f019b27) |
| 6         | Enhancer        | H3K4me1 H2AFZ H3K4me2                  | +-           | - Немного выражен на границах              | +- Больше выражу к концу | +- | Достаточно сильный сигнал для H3K4me1,то есть связан с усилителями генов, в геноме встречается редко маленькими отрезками    | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/e97ed084-2c3b-45ae-847c-97e00f019b27) |
| 7         | Enhancer        | H3K4me1 H3K27ac H3K4me2 H3K9ac H2AFZ H3K4me3 | -      | +- Немного выражен на границах             | +- Больше к концам| +- | Редко встречается в геноме, сильный сигнал для всех указанных меток (но наиболее сильный для H3K4me1 - ассоциация с усилителями генов), небольшая ассоциация с TES | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/e720863f-a738-4faf-b3bf-4d08e843dadf) |
| 8         | Promoter        | Со всеми кроме H3K27ac H4K20me1 H3K79me2 H3K36me3 | +- | +- В центре хорошо выражено               | +- лучше выражено до | +- | Редко встречается, сигнал сильная и для H3K4me2 и для H3K4me3, много в начале последовательности | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/2b6ff0e1-3f98-40be-af30-499c14019528) |
| 9         |  Promoter       | Cо всеми кроме H4K20me1 H3K79me2 H3K36me3  | + | + В центре выражено лучше | + Выражено лучше после| - | Редко встречается в геноме, сигнал сильный для H3K4me2 и H3K4me3 + много в начале транскрипции, ассоциация с TES и TSS | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/dac61602-cb48-43c0-8b05-335f23248ce0) |
| 10       |  Promoter       | Cо всеми | +- | + В центре выражено лучше | + Выражено лучше после| + Выражено лучше до | - | Редко встречается в геноме, сигнал сильный для H3K4me2 и H3K4me3 + много в начале транскрипции, ассоциация с TES и TSS | ![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/6a5946ff-58b4-40b4-8856-090647115237) |

Ну и данные совпали с графиком похожести: 4, 5 примерно похожи, 6 и 7 тоже, 8, 9 и 10 тоже вместе. 

## Бонус

Стало действительно понятнее
![image](https://github.com/polipolinom/hse_hw3_chromhmm/assets/77383801/f09dec99-3651-4296-80fc-7412395c9ff5)

Все команды можно и нужно смотреть в ноутбуке, других не выполнялось.

