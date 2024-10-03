# -*- coding: utf-8 -*-
"""
Created on Thu Oct  3 15:29:14 2024

@author: stian
"""

import csv
from datetime import datetime, timedelta
import matplotlib.pyplot as plt

# Function to calculate moving average
def moving_average(times, temperatures, n):
    avg_times = []
    avg_temps = []
    for i in range(n, len(temperatures) - n):
        avg_times.append(times[i])
        avg_temps.append(sum(temperatures[i - n:i + n + 1]) / (2 * n + 1))
    return avg_times, avg_temps

# Initialiser fem tomme lister
Datoliste, Sekundliste, list3, list4, list5 = [], [], [], [], []

# Åpne CSV-filen
with open('trykk_og_temperaturlogg_rune_time.csv.txt', newline='') as csvfile:
    csvreader = csv.reader(csvfile, delimiter=';')

    # Gå gjennom hver rad i CSV-filen
    for row in csvreader:
        if len(row) == 5:
            if not any("am" in cell.lower() or "pm" in cell.lower() for cell in row):
                Datoliste.append(row[0])
                Sekundliste.append(row[1])
                list3.append(row[2])
                list4.append(row[3])
                list5.append(row[4])

del Datoliste[0]
del Sekundliste[0]
del list3[0]
del list4[0]
del list5[0]

# Liste for å lagre de kombinerte tidsverdiene
tidsverdier = []

# Gå gjennom begge listene samtidig
for dt_str, sekunder in zip(Datoliste, Sekundliste):
    # Konverter strengen til et datetime-objekt
    dt_obj = datetime.strptime(dt_str, "%m.%d.%Y %H:%M")

    # Legg til sekundene
    dt_obj += timedelta(seconds=int(sekunder))

    # Legg til den kombinerte tidsverdien i listen
    tidsverdier.append(dt_obj)

tull1, tull2, tidfil2, tempfil2, trykkfil2 = [], [], [], [], [] 
with open('temperatur_trykk_met_samme_rune_time_datasett.csv.txt', newline='') as csvfile:
    csvreader = csv.reader(csvfile, delimiter=';')

    # Gå gjennom hver rad i CSV-filen
    for row in csvreader:
        if len(row) == 5:
                tull1.append(row[0])
                tull2.append(row[1])
                tidfil2.append(row[2])
                tempfil2.append(row[3])
                trykkfil2.append(row[4])  

del tull1
del tull2
del tidfil2[0]
del tidfil2[-1]
del tempfil2 [0]
del tempfil2[-1]
del trykkfil2 [0]
del trykkfil2[-1]

tidfil2 = [datetime.strptime(tid, "%d.%m.%Y %H:%M") for tid in tidfil2]

tempfil2 = [float(temp.replace(',', '.')) for temp in tempfil2]
list5 = [float(value.replace(',', '.')) for value in list5]

# Calculate moving average for n=30
n = 30
avg_times, avg_temps = moving_average(tidsverdier, list5, n)

# Lag en figur og en akse
fig, ax = plt.subplots()

# Plott temperaturdataene fra den første filen
ax.plot(tidsverdier, list5, label='Temperatur fra første fil', color='blue')

# Plott temperaturdataene fra den andre filen
ax.plot(tidfil2, tempfil2, label='Temperatur fra andre fil', color='green')

# Plott gjennomsnittsverdiene
ax.plot(avg_times, avg_temps, label='Gjennomsnittstemperatur (n=30)', color='orange')

# Legg til etiketter og tittel
ax.set(xlabel='Tid', ylabel='Temperatur',
       title='Temperatur over Tid fra to forskjellige filer')

# Legg til en legende
ax.legend()

# Roter datoetikettene for bedre lesbarhet
plt.xticks(rotation=45)

# Juster layout for å unngå overlapp
plt.tight_layout()

# Vis grafen
plt.show()
