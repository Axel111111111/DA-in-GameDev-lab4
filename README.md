# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4

"РАЗРАБОТКА СИСТЕМЫ МАШИННОГО ОБУЧЕНИЯ."

Выполнил:
- Зубов Алексей Иванович
- РИ-210946

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.


Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.

Ход работы:

Шаг 1 Создаём и активируем нового ML-агента, а также скачиваем необходимые библиотеки.

![1](https://user-images.githubusercontent.com/49406824/197343257-8f39dde6-ace4-4ed9-94fa-888342e5a4c4.png)

Шаг 2 Создаём на сцене плоскость, куб и сферу. Создаём простой C# скрипт-файл и подключаем его к сфере. В скрипт-файл RollerAgent.cs добавляем 
код, опубликованный в материалах лабораторных работ. Объекту «сфера» добавляем компоненты Rigidbody, Decision Requester, Behavior Parameters и настраиваем их.

![2](https://user-images.githubusercontent.com/49406824/197343370-db95d526-fd0b-4feb-bd03-733c3524e67b.png)

![3](https://user-images.githubusercontent.com/49406824/197343420-5776ca09-39ff-455d-b358-3cf101382f42.png)


Шаг 3 В корень проекта добавляум файл конфигурации нейронной сети, доступный в папке с файлами проекта. Запускаем  ml-агента. Запускаем сцену в Unity
и проверяем работу ML-Agent’a.

        behaviors:
        RollerBall:
         trainer_type: ppo
         hyperparameters:
           batch_size: 10
           buffer_size: 100
           learning_rate: 3.0e-4
           beta: 5.0e-4
           epsilon: 0.2
           lambd: 0.99
           num_epoch: 3
           learning_rate_schedule: linear
         network_settings:
           normalize: false
           hidden_units: 128
           num_layers: 2
         reward_signals:
           extrinsic:
             gamma: 0.99
             strength: 1.0
         max_steps: 500000
         time_horizon: 64
         summary_freq: 10000

Шаг 4 Делаем 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запускаем симуляцию сцены и наблюдаем за результатом обучения модели. После завершения 
обучения проверяем работу модели.

![4](https://user-images.githubusercontent.com/49406824/197343553-b5d0be6c-da1e-4020-900f-3ded9c347851.png)

![5](https://user-images.githubusercontent.com/49406824/197343642-08bcbf97-abe9-47b8-a349-5f1f9696694f.png)

## Выводы

При увеличении количества агентов в Unity модель достигает более высоких показателей точности за меньшее время итераций.

## Задание 2
Подробно опсали каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно
нашли информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.

      behaviors: #cоздание списка "Модель поведения" дял разных агентов
       RollerBall: #cоздание списка конкретного объекта
         trainer_type: ppo #ppo - это алгоритм обучения с подкреплением от OpenAi
         hyperparameters:
           batch_size: 10 #количество опыта на каждоый итерации
           buffer_size: 100 #колличество опыта которое необхдимо собрать для перехода к обучению или изучении модели
           learning_rate: 3.0e-4 #скорость обучения
           beta: 5.0e-4
           epsilon: 0.2
           lambd: 0.99
           num_epoch: 3
           learning_rate_schedule: linear #определение изменения скорости обучения с течением времени
         network_settings:
           normalize: false #к входным данным не применяется нормализация
           hidden_units: 128 #количество нейронов в слоях нейронной сети
           num_layers: 2 #количество слоев нейроной сети
         reward_signals: #настройка сигналов вознаграждения
           extrinsic:
             gamma: 0.99
             strength: 1.0 #коэффициент вознаграждения
         max_steps: 500000 #количество шагов для завершения обучения
         time_horizon: 64 #количество шагов для добавления в буфер опыта
         summary_freq: 10000 #количество шагов для создавния и вывода статистикиобучения
    
### Decision Requester
запрос на принятие решения вызывает CollectObservation, а затем получает последнее действие в OnActionReceived, основанное на этом новом собранном наблюдении. С действиями из TakeActionBetweenDecisions он только снова вызовет OnActionReceived без сбора новых наблюдений и выведет последнее действие, которое он получил от NN.

### Behavior Parameters
Параметры поведения — У каждого Агента должно быть определенное поведение. Поведение определяет, как Агент принимает решения. Максимальный шаг — Определяет, сколько шагов моделирования может произойти до окончания эпизода Агента.
    

## Задание 3
### Дорабатываем сцену и обучфем ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны случайно изменять координаты на плоскости.

Доработали сцену и обучили ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Добавим еще один куб. Создадим код, в котором 
опишим перемещение шара между двумя кубиками разного цвета

        using System.Collections;
        using System.Collections.Generic;
        using UnityEngine;
        using Unity.MLAgents;
        using Unity.MLAgents.Sensors;
        using Unity.MLAgents.Actuators;

        public class Move : Agent
        {
            [SerializeField] private GameObject goldMine;
            [SerializeField] private GameObject village;
            private float speedMove;
            private float timeMining;
            private float month;
            private bool checkMiningStart = false;
            private bool checkMiningFinish = false;
            private bool checkStartMonth = false;
            private bool setSensor = true;
            private float amountGold;
            private float pickaxeСost;
            private float profitPercentage;
            private float[] pricesMonth = new float[2];
            private float priceMonth;
            private float tempInf;

            // Start is called before the first frame update
            public override void OnEpisodeBegin()
            {
                // If the Agent fell, zero its momentum
                if (this.transform.localPosition != village.transform.localPosition)
                {
                    this.transform.localPosition = village.transform.localPosition;
                }
                checkMiningStart = false;
                checkMiningFinish = false;
                checkStartMonth = false;
                setSensor = true;
                priceMonth = 0.0f;
                pricesMonth[0] = 0.0f;
                pricesMonth[1] = 0.0f;
                tempInf = 0.0f;
                month = 1;
            }
            public override void CollectObservations(VectorSensor sensor)
            {
                sensor.AddObservation(speedMove);
                sensor.AddObservation(timeMining);
                sensor.AddObservation(amountGold);
                sensor.AddObservation(pickaxeСost);
                sensor.AddObservation(profitPercentage);
            }

            public override void OnActionReceived(ActionBuffers actionBuffers)
            {
                if (month < 3 || setSensor == true)
                {
                    speedMove = Mathf.Clamp(actionBuffers.ContinuousActions[0], 1f, 10f);
                    Debug.Log("SpeedMove: " + speedMove);
                    timeMining = Mathf.Clamp(actionBuffers.ContinuousActions[1], 1f, 10f);
                    Debug.Log("timeMining: " + timeMining);
                    setSensor = false;
                    if (checkStartMonth == false)
                    {
                        Debug.Log("Start Coroutine StartMonth");
                        StartCoroutine(StartMonth());
                    }

                    if (transform.position != goldMine.transform.position & checkMiningFinish == false)
                    {
                        transform.position = Vector3.MoveTowards(transform.position, goldMine.transform.position, Time.deltaTime * speedMove);
                    }

                    if (transform.position == goldMine.transform.position & checkMiningStart == false)
                    {
                        Debug.Log("Start Coroutine StartGoldMine");
                        StartCoroutine(StartGoldMine());
                    }

                    if (transform.position != village.transform.position & checkMiningFinish == true)
                    {
                        transform.position = Vector3.MoveTowards(transform.position, village.transform.position, Time.deltaTime * speedMove);
                    }

                    if (transform.position == village.transform.position & checkMiningStart == true)
                    {
                        checkMiningFinish = false;
                        checkMiningStart = false;
                        setSensor = true;
                        amountGold = Mathf.Clamp(actionBuffers.ContinuousActions[2], 1f, 10f);
                        Debug.Log("amountGold: " + amountGold);
                        pickaxeСost = Mathf.Clamp(actionBuffers.ContinuousActions[3], 100f, 1000f);
                        Debug.Log("pickaxeСost: " + pickaxeСost);
                        profitPercentage = Mathf.Clamp(actionBuffers.ContinuousActions[4], 0.1f, 0.5f);
                        Debug.Log("profitPercentage: " + profitPercentage);

                        if (month != 2)
                        {
                            priceMonth = pricesMonth[0] + ((pickaxeСost + pickaxeСost * profitPercentage) / amountGold);
                            pricesMonth[0] = priceMonth;
                            Debug.Log("priceMonth: " + priceMonth);
                        }
                        if (month == 2)
                        {
                            priceMonth = pricesMonth[1] + ((pickaxeСost + pickaxeСost * profitPercentage) / amountGold);
                            pricesMonth[1] = priceMonth;
                            Debug.Log("priceMonth: " + priceMonth);
                        }

                    }
                }
                else
                {
                    tempInf = ((pricesMonth[1] - pricesMonth[0]) / pricesMonth[0]) * 100;
                    if (tempInf <= 6f)
                    {
                        SetReward(1.0f);
                        Debug.Log("True");
                        Debug.Log("tempInf: " + tempInf);
                        EndEpisode();
                    }
                    else
                    {
                        SetReward(-1.0f);
                        Debug.Log("False");
                        Debug.Log("tempInf: " + tempInf);
                        EndEpisode();
                    }
                }
            }

            IEnumerator StartGoldMine()
            {
                checkMiningStart = true;
                yield return new WaitForSeconds(timeMining);
                Debug.Log("Mining Finish");
                checkMiningFinish = true;
            }

            IEnumerator StartMonth()
            {
                checkStartMonth = true;
                yield return new WaitForSeconds(60);
                checkStartMonth = false;
                month++;

            }
        }

## Выводы

Игровой баланс - ключевое понятие в играх, когда различные игровые объекты взаимодействуют друг с другом на уровне правил игры. Нет универсального правила, каким должен быть баланс в каждой конкретной игре, есть лишь парадигмы, которые описывают общее положение введения баланса. Однако, чем лучше в игре проработан баланс, тем больше игра становится "играбельной" и понятнее для игрока. Такие аспекты, как игровая экономика, различия между героями игры, взаимодейстие механик персонажей с пространством, взаимодействие игроков с другими игроками - первые в списке, которые подлежат балансу.
Существует 2 основных игровых системы: симметричные игры, где обе стороны начинают с одинаковыми условиями, и асимметричные.
Cуществует 2 парадигмы: метод от образа и от характеристик. Первый - создание характеристик от уже нарисованного персонажа по внешнему виду или лору персонажа. Второй - создание персонажа и его лора по уже заданным характеристикам. Машинное обучение в таких случаях позволяет более точно распределять игровые механики, которые подлежаь балансу.

**BigDigital Team: Denisov | Fadeev | Panov**
