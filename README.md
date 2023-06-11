# 3
Парсер цены пшеница 

import requests
from urllib.request import urlopen
from lxml import etree
from bs4 import BeautifulSoup
import time
import tkinter as tk
import threading

##cont = 0

def run_parser():
##    global cont

    while True:
        url = 'https://rif-rostov.ru/price/filter/127/0/0/single/'
        response2 = requests.post(url)
        html2 = response2.text
        with open('star_wars4', 'w', encoding='utf-8') as f:
            f.write(html2)

        soup = BeautifulSoup(html2, 'lxml')
        table = soup.find('table')
        second_row = table.find_all('tr')[2]
        second_cell_value = second_row.find_all('td')[0].text
        nam_str = "".join(filter(str.isdigit, second_cell_value))
    

##        cont += 1

##        print(second_cell_value)
##        print(cont)

##        label2.config(text=cont)  # обновление значения счетчика на лейбле

        label3.config(text=nam_str, font=('Arial', 50))  # обновление значения лейбла с данными

        time.sleep(16)  # задержка на 16 секунд перед повторным запросом и обновлением данных

root = tk.Tk()
root.title('Парсер пшеницы')
root.geometry('350x350')

label1 = tk.Label(root, text='Цена пшеница 1 сорт РИФ:')
label1.pack()

##label2 = tk.Label(root, text=cont)
##label2.pack()

label3 = tk.Label(root, text='', font=('Arial', 50))  # создание пустого лейбла для отображения данных
label3.pack(anchor='center', padx=40, pady=30)

labe4 = tk.Label(text='спонсор разработки \n    сайт Stoptut.ru ♥(Профессиональные рации)', font=("Times New Roman", 8),foreground='Blue')
labe4.pack(anchor='center', padx=40, pady=70)
##        ) 

thread = threading.Thread(target=run_parser)  # запуск цикла while True в отдельном потоке
thread.start()

root.mainloop()  # вызов главного цикла Tkinter в начале кода
