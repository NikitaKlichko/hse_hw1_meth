# Домашнее задание № 1. Метилирование. 

###### Кличко Никита 

*Ссылка на* [google colab](https://colab.research.google.com/drive/1cLTOv34dX2CA6wlvN2Z44syi1jDfigOk?usp=sharing) 

## Часть 1. Анализ FastQC. 
| BS-seq | RNA-seq | 
--- | ---  
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/icm_stats.PNG) | ![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/rna_stat.PNG) | 
 
 Из статистики видно, что процент содержания GC у РНК почти в два раза выше чем у BS-seq.
 
| BS-seq | RNA-seq | 
--- | ---  
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/icm_per_base.PNG) | ![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/rna_per_base.PNG) |  

На первом графике содержание Цитозина меньше чем на втором и составляет около 5%. Содержание Тимина в первом случае выше, а Гуанина немного ниже.

| BS-seq | RNA-seq | 
--- | ---  
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/icm_per_seq.PNG) | ![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/rna_per_seq.PNG) | 

Первое распределение по сравнению со вторым имеет явные отклонения от нормального, два пика и смещение в левую сторону. 

## Часть 2 

### a and b

| Samples | chr11:11347700-11367700| chr11:40185800-40195800 | deduplication ( % ) |  
--- | --- | --- | ---  
8 cell | 1090	 | 464 | 81.69 |  
Epiblast | 2328 | 1062 | 97.08 |  
ICM | 1456 | 630	 | 90.92 | 

*bash-scipt:*
```
! ls *pe.bam | xargs -P 4 -tI{} deduplicate_bismark  --bam  --paired  -o s_{} {} 
```

### c 
Коллинг проведен 

### d 
Отчеты в [html](https://github.com/NikitaKlichko/hse_hw1_meth/tree/main/html)

**8Cell** 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/8cell1.PNG) 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/8cell2.PNG) 

**Epiblast** 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/epiblast1.PNG) 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/epiblast2.PNG) 

**ICM** 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/icm1.PNG) 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/icm2.PNG) 
**Отчет**  
Данные графики-графики смещения метиллирования, которые показывают пропорции метиллирования по каждому положению в прочтении. У нас парные чтения, вследствие чего мы можем наблюдать два графика для каждого образца. Исходя из графиков можно выявить смещение 3’-end-repair начальных позиций в двух прочтениях paired-end reads.
### e 

*Code:* 
```python
sns.set_style("darkgrid")
ind = ['SRR5836473', 'SRR3824222', 'SRR5836475']
samples = ['8cell', 'Epiblast', 'ICM']
for i, s in zip(ind, samples):
    name = 's_' + i + '_1_bismark_bt2_pe.deduplicated.bedGraph'
    df = pd.read_csv(name, delimiter='\t', skiprows=1, header=None)
    fig = plt.figure(figsize=(10, 7))
    plt.hist(df[3], density=True, bins=100)
    plt.title('Метиллирование цитозинов образца {}'.format(s))
    plt.xlabel('Процент метиллирования цитозинов')
    plt.ylabel('Частота')
    plt.show()
``` 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/freq_8cell.png) 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/frea_epiblast.png) 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/freq_icm.png) 

### f 

**Уровень метиллирования** 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/methyl2.png) 

**Уровень покрытия** 
![](https://github.com/NikitaKlichko/hse_hw1_meth/blob/main/imgs/covered.png)
