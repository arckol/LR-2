# Инструменты анализа данных в примерах и задачах
Отчет по лабораторной работе #2 выполнил:
- Колин Арсений Витальевич
- РИ-210943

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |



## Цель работы
Сбор, обработка и визуализация тестового набора данных

## Скриншоты
Скриншоты с выполнением всех заданий: https://disk.yandex.ru/d/BkqkaS5WJ7R2iQ

## Код для заданий 1, 2, 3

```py

In [ ]:

import gspread
import numpy as np
gc = gspread.service_account(filename='/Users/arseniikolin/PycharmProjects/UnityDataScience/unitydatasciense-379613-43b69ef0767a.json')
sh = gc.open("UnitySheets")
price = np.random.randint(200, 10000, 11)
mon = list(range(1, 11))
i = 0
while i <= len(mon):
    i += 1
    if i ==0:
        continue
    else:
        tempInf = ((price[i-1] - price[i-2]) / price[i-2])*100
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.',',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i-1]))
        sh.sheet1.update(('C' + str(i)), str(tempInf))
        print(tempInf)


```



```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
   public AudioClip goodSpeak;
   public AudioClip normalSpeak;
   public AudioClip badSpeak;
   private AudioSource selectAudio;
   private Dictionary<string, float> dataSet = new Dictionary<string, float>();
   private bool statusStart = false;
   private int i = 1;
    // Start is called before the first frame update
   void Start()
   {
        StartCoroutine(GoogleSeets());
   }

    // Update is called once per frame
   void Update()
   {
      if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
      {
         StartCoroutine(PlaySelectAudioGood());
         Debug.Log(dataSet["Mon_" + i.ToString()]);
      }

      if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] < 100 & statusStart == false & i != dataSet.Count)
      {
         StartCoroutine(PlaySelectAudioNormal());
         Debug.Log(dataSet["Mon_" + i.ToString()]);
      }

      if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
      {
         StartCoroutine(PlaySelectAudioBad());
         Debug.Log(dataSet["Mon_" + i.ToString()]);
      }
   }

   IEnumerator GoogleSeets()
   {
      UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1-_G6AOTaXzTOG8JcH9sDV00LtjhVP_7iZgISxJYr7Wg/values/Лист1?key=AIzaSyBU5nM93vFbK_ksuzRVxspyn50GqXAgzxo");
      yield return curentResp.SendWebRequest();
      string rawResp = curentResp.downloadHandler.text;
      var rawJson = JSON.Parse(rawResp);
      foreach (var itemRawJson in rawJson["values"])
      {
         var parseJson = JSON.Parse(itemRawJson.ToString());
         var selectRow = parseJson[0].AsStringList;
         dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
      }   
   }

   IEnumerator PlaySelectAudioGood()
   {
      statusStart = true;
      selectAudio = GetComponent<AudioSource>();
      selectAudio.clip = goodSpeak;
      selectAudio.Play();
      yield return new WaitForSeconds(3);
      statusStart = false;
      i++;
   }
   IEnumerator PlaySelectAudioNormal()
   {
      statusStart = true;
      selectAudio = GetComponent<AudioSource>();
      selectAudio.clip = normalSpeak;
      selectAudio.Play();
      yield return new WaitForSeconds(3);
      statusStart = false;
      i++;
   }
   IEnumerator PlaySelectAudioBad()
   {
      statusStart = true;
      selectAudio = GetComponent<AudioSource>();
      selectAudio.clip = badSpeak;
      selectAudio.Play();
      yield return new WaitForSeconds(4);
      statusStart = false;
      i++;
   }
}

```


## Выводы

В этой лабораторной работе я научился добавлять автоматически данные полученные результатом выполнения кода, научился совмещать работу Unity, PyCharm and VS code. 


