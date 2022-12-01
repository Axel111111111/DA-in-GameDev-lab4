# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4

"Перцептрон"

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


## Задание 1
## В проекте Unity реализовать перцептрон, который умеет производить вычисления:

Во время вычислений я проверял количество ошибок при 2, 4, 5, 6, 8 эпохах и пытался найти значение эпох при котором перцептрон полностью обучится.
Во время тыстов я брал выборку из 10 попыток (в некоторых случаях из 30)

### OR

![1 1 1](https://user-images.githubusercontent.com/49406824/205069019-2de446b0-9d23-4d16-856d-dca22a6cbe15.png)
<br>
Количество эпох: 2 <br>
Количество успешных обучений: 1/10 <br><br>
![1 1 2](https://user-images.githubusercontent.com/49406824/205069042-0e2d6367-3c89-482d-a0de-c91e337f0239.png)
<br>
Количество эпох: 4 <br>
Количество успешных обучений: 7/10 <br><br>
![1 1 3](https://user-images.githubusercontent.com/49406824/205069074-048affa9-d5b5-4d8e-8284-5c8e57e742ff.png)
<br>
Количество эпох: 5 <br>
Количество успешных обучений: 9/10 <br><br>
![1 1 3](https://user-images.githubusercontent.com/49406824/205069084-e8faefca-a044-46ea-8429-6ee7ebe2eed4.png)
<br>
Количество эпох: 6 <br>
Количество успешных обучений: 30/30 <br><br>
![1 1 4](https://user-images.githubusercontent.com/49406824/205069107-e4839ece-e319-4bc1-82d7-69f4014d4fa9.png)
<br>

### AND

![1 2 1](https://user-images.githubusercontent.com/49406824/205069142-6eb8ef8a-815e-49f3-a0a7-5cb1808507de.png)
<br>
Количество эпох: 4 <br>
Количество успешных обучений: 0/10 <br><br>
![1 2 2](https://user-images.githubusercontent.com/49406824/205069160-8b696e82-ed8c-4251-ab0e-c9dc8ced3632.png)
<br>
Количество эпох: 6 <br>
Количество успешных обучений: 4/10 <br><br>
![1 2 3](https://user-images.githubusercontent.com/49406824/205069180-20327a44-1c9e-48e3-98b8-2de8fb8656e1.png)
<br>
Количество эпох: 8 <br>
Количество успешных обучений: 25/30 <br><br>
![1 2 4](https://user-images.githubusercontent.com/49406824/205069196-9a9e346d-0285-403a-a503-a4d3bc14ab99.png)
<br>

### NAND

![1 3 1](https://user-images.githubusercontent.com/49406824/205069212-0bb715a3-f7c2-43fb-9fd1-597e164e5f4e.png)
<br>
Количество эпох: 4 <br>
Количество успешных обучений: 2/10<br><br>
![1 3 2](https://user-images.githubusercontent.com/49406824/205069266-feac7f60-acbf-42d8-8df0-3cd05d3e8446.png)
<br>
Количество эпох: 6 <br>
Количество успешных обучений: 4/10<br><br>
![1 3 3](https://user-images.githubusercontent.com/49406824/205069286-0b6ee32c-5312-443d-9bfa-9e7e8427c2e5.png)
<br>
Количество эпох: 8 <br>
Количество успешных обучений: 27/30<br><br>
![1 3 4](https://user-images.githubusercontent.com/49406824/205069304-15b642fb-5d25-48ca-bfe8-6f1743405c5b.png)
<br>

### XOR

У XOR перцептрон не может выполнить вычисления <br><br>
![1 4 1](https://user-images.githubusercontent.com/49406824/205069323-5f88cb16-a7cf-446b-aacf-9aa76daf755c.png)
![1 4 2](https://user-images.githubusercontent.com/49406824/205069335-7d00640d-a18b-4528-94dd-6b3cd087fb79.png)
<br>


## Задание 2
## Построить график зависимочти количества эпох от количества ошибк обучения. Указать от чего зависит необходимое количество эпох обучения
<br>

![2 1](https://user-images.githubusercontent.com/49406824/205069813-c2c46fc1-0365-4de1-90f8-c38555c646ac.png)

![2 2](https://user-images.githubusercontent.com/49406824/205069830-5567fd89-5229-4b6c-978c-1de48ecf91b3.png)

Необходимое количество эпох обучения зависит от bias - смещение и weights - веса. Доказательство можно увидеть в коде ниже:

'double DotProductBias(double[] v1, double[] v2) 
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
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}'

## Задание 3
## Построить визуальную модель работы перцептрона на сцене Unity






## Выводы



**BigDigital Team: Denisov | Fadeev | Panov**
