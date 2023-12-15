# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Шайхутдинов Рамазан Шамильевич;
- РИ-220948

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Изучить работу перцептрона в среде Unity

## Задание 1
### в проекте Unity реализовать перцептрон, который умеет производить вычисления:
### OR | 0+0=0 0+1=1 1+0=1 1+1=1
### AND | 0+0=0 0+1=0 1+0=0 1+1=1
### NAND | 0+0=1 0+1=1 1+0=1 1+1=0
### XOR | 0+0=0 0+1=1 1+0=1 1+1=0

Ход работы:
- Сперва создал проект Unity, добавил пустой GameObject и добавил скрипт Perceptron.cs из предоставленного репозитория.
- После запуска проекта, в консоли появились логи с информацией: 

- Для OR:
![image](https://github.com/knightalli/DAinGD-lab4/assets/127225486/f3617045-cd57-42fc-a1a4-1edc2e7bb1ac)

- Для AND:
![image](https://github.com/knightalli/DAinGD-lab4/assets/127225486/f3617045-cd57-42fc-a1a4-1edc2e7bb1ac)

- Для NAND:
![image](https://github.com/knightalli/DAinGD-lab4/assets/127225486/f3617045-cd57-42fc-a1a4-1edc2e7bb1ac)

- Для XOR:
![image](https://github.com/knightalli/DAinGD-lab4/assets/127225486/f3617045-cd57-42fc-a1a4-1edc2e7bb1ac)

- Скрипт Персептрона из репозитория:
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
    public double[] input;
    public double output;
}

public class Perceptron : MonoBehaviour
{

    public TrainingSet[] ts;
    double[] weights = { 0, 0 };
    double bias = 0;
    double totalError = 0;

    double DotProductBias(double[] v1, double[] v2)
    {
        if (v1 == null || v2 == null)
            return -1;

        if (v1.Length != v2.Length)
            return -1;

        double d = 0;
        for (int x = 0; x < v1.Length; x++)
        {
            d += v1[x] * v2[x];
        }

        d += bias;

        return d;
    }

    double CalcOutput(int i)
    {
        double dp = DotProductBias(weights, ts[i].input);
        if (dp > 0) return (1);
        return (0);
    }

    void InitialiseWeights()
    {
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = Random.Range(-1.0f, 1.0f);
        }
        bias = Random.Range(-1.0f, 1.0f);
    }

    void UpdateWeights(int j)
    {
        double error = ts[j].output - CalcOutput(j);
        totalError += Mathf.Abs((float)error);
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = weights[i] + error * ts[j].input[i];
        }
        bias += error;
    }

    double CalcOutput(double i1, double i2)
    {
        double[] inp = new double[] { i1, i2 };
        double dp = DotProductBias(weights, inp);
        if (dp > 0) return (1);
        return (0);
    }

    void Train(int epochs)
    {
        InitialiseWeights();

        for (int e = 0; e < epochs; e++)
        {
            totalError = 0;
            for (int t = 0; t < ts.Length; t++)
            {
                UpdateWeights(t);
                Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
            }
            Debug.Log("TOTAL ERROR: " + totalError);
        }
    }

    void Start()
    {
        Train(8);
        Debug.Log("Test 0 0: " + CalcOutput(0, 0));
        Debug.Log("Test 0 1: " + CalcOutput(0, 1));
        Debug.Log("Test 1 0: " + CalcOutput(1, 0));
        Debug.Log("Test 1 1: " + CalcOutput(1, 1));
    }

    void Update()
    {

    }
}
```

## Задание 2
###  Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.
- Я собрал информацию с логов после каждого запуска персептрона для всех логических случаев:
- Персептрон отлично обучается, к 6 эпохе не делает ошибок, кроме случая в XOR, с повышением эпохи делает ошибок больше:

![image](https://github.com/knightalli/DAinGD-lab4/assets/127225486/058b7773-5643-4160-950a-0e25dd2bead9)



## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.
-

## Выводы
Я реализовал персептрон на пустом GameObject'е, а также проанализировал обучение с разным количеством эпох и построил график на полученных данных.

## Powered by

Шайхутдинов Р.
