# Домашнее задание № 1. Метилирование. 

###### Кличко Никита 

## Часть 1. Анализ FastQC.

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
