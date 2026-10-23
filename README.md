# Сценарии iptables<br><br>
Описание/Пошаговая инструкция выполнения домашнего задания:<br><br>
1.	реализовать knocking port<br>
•	centralRouter может попасть на ssh inetrRouter через knock скрипт.
пример в материалах.<br>
2.	добавить inetRouter2, который виден(маршрутизируется (host-only тип сети для виртуалки)) с хоста или форвардится порт через локалхост.<br>
3.	запустить nginx на centralServer.<br>
4.	пробросить 80й порт на inetRouter2 8080.<br>
5.	дефолт в инет оставить через inetRouter.<br><br>
__________________________________________________________________________________________________________________________________
Схема сети:<br><br>
<img width="519" height="587" alt="image" src="https://github.com/user-attachments/assets/1c57c9fd-0a12-4f87-b758-e61f3d79bce0" /><br><br>
<i>В схеме забыл дорисовать сеть для хоста 192.168.56.0/24 на inetRouter2, но она есть.</i><br><br>
1-2.	За основу берем инфраструктуру из [прошлого ДЗ](https://github.com/mrigorevich/lan_laboratory).<br>
В [обновленном Vagrantfile](https://github.com/mrigorevich/iptables_scenario/blob/main/Vagrantfile) закомментированы лишние хосты (включая работающий ansible), добавлен inetRouter2.<br>
Измененные файлы ansible: <br>
[inventory.ini](https://github.com/mrigorevich/iptables_scenario/blob/main/inventory.ini) <br>
[setup_routers2.yml](https://github.com/mrigorevich/iptables_scenario/blob/main/setup_routers2.yml) <br>
[save_netplan2.yml](https://github.com/mrigorevich/iptables_scenario/blob/main/save_netplan2.yml)<br>
После применения имеем следующие правила на inetRouter:<br><br>
<img width="974" height="471" alt="image" src="https://github.com/user-attachments/assets/9927d63c-f191-4556-af73-26f1dc49f752" /><br><br>
Безусловно разрешаем порт 22 с основного хоста и с ВМ ansible. Вход с centralRouter через Knock, остальные входящие на 22 порт закрываем.<br>
На ВМ centralRouter:<br>
`nano knock_knock.sh` # создаем скрипт подключения<br><br>
<img width="549" height="489" alt="image" src="https://github.com/user-attachments/assets/c3c065df-834f-4a5d-a016-755372e12e98" /><br><br>
Сохраняем, делаем исполняемым и запускаем:<br><br>
<img width="607" height="255" alt="image" src="https://github.com/user-attachments/assets/486b491c-3384-45f0-9b1c-df9077edc26b" /><br><br>
Отключаемся и пробуем подключиться без knock-скрипта:<br><br>
<img width="570" height="140" alt="image" src="https://github.com/user-attachments/assets/b27adf52-04d9-45dc-8a0f-218729791e84" /><br><br>
Подключение не происходит. Задание 1 готово.<br>
На ВМ inetRouter2:<br><br>
<img width="974" height="265" alt="image" src="https://github.com/user-attachments/assets/02ce1eac-fb5f-49e2-b84f-4e4c57cd498e" /><br><br>
<img width="974" height="145" alt="image" src="https://github.com/user-attachments/assets/da4be3c6-e811-41a8-8195-f208437ee026" /><br><br>
Задание 2 готово.<br>
3.	Проверяем как отработал ansible на centralServer:<br><br>
<img width="974" height="300" alt="image" src="https://github.com/user-attachments/assets/8a8513a6-d751-4a81-a810-d962d3ecb63b" /><br><br>
Задание 3 готово.<br>
4.	Проверяем маршрут с inetRouter2 до centralServer и доступность nginx с хоста:<br><br>
<img width="974" height="115" alt="image" src="https://github.com/user-attachments/assets/02269e24-1eb2-47d1-91f1-7a4243e4ae85" /><br><br>
<img width="640" height="326" alt="image" src="https://github.com/user-attachments/assets/8e086efe-abc3-4190-97fd-3b0815ccd9ac" /><br><br>
5. 	Проверяем маршруты на centralServer:<br><br>
<img width="974" height="342" alt="image" src="https://github.com/user-attachments/assets/e91b349f-22c3-422c-8ab4-8b445c5617b6" />


