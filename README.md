# Authorization-and-authentication
Authorization and authentication


- Запретить всем пользователям, кроме группы admin логин в выходные (суббота и воскресенье), без учета праздников

- Дать конкретному пользователю права работать с докером и возможность рестартить докер сервис*

---

### Запретить всем пользователям, кроме группы admin логин в выходные (суббота и воскресенье), без учета праздников.

Дано:

![image](https://github.com/user-attachments/assets/172cc13e-c0c9-44ae-b1dd-1782c98dc88b)


( Шаги с методички, vagrant не используется)

1. Создаём пользователя otusadm и otus:

sudo useradd otusadm && sudo useradd otus

3. Создаём пользователям пароли:

echo "Otus2022!" | sudo passwd --stdin otusadm && echo "Otus2022!" | sudo passwd --stdin otus

Для примера мы указываем одинаковые пароли для пользователя otus и otusadm

4. Создаём группу admin:

sudo groupadd -f admin

5. Добавляем пользователей root и otusadm в группу admin:

usermod otusadm -a -G admin && usermod root -a -G admin

7. Проверим, что пользователи root  и otusadm есть в группе admin:

![image](https://github.com/user-attachments/assets/cfb85b6c-fc37-4dd5-a7d5-19ad7d219998)

8. Создадим файл-скрипт /usr/local/bin/login.sh

![image](https://github.com/user-attachments/assets/79469f87-2cb2-4c99-b2cf-ddd858bc053c)

9. Добавим права на исполнение файла: chmod +x /usr/local/bin/login.sh

10. Укажем в файле /etc/pam.d/sshd модуль pam_exec и наш скрипт:

vim /etc/pam.d/sshd 

![image](https://github.com/user-attachments/assets/495ba679-c7e4-4d4d-bea9-0924e740d924)


Финальная првоверка:


![image](https://github.com/user-attachments/assets/4c9887d6-ac55-44a9-8747-874f8d80db95)

---

### Дать конкретному пользователю права работать с докером и возможность рестартить докер сервис*

Просто сделаем это через sudors.d :

![image](https://github.com/user-attachments/assets/2c19da44-396f-4ab0-919f-04ec4b56e75a)



Добавлем его в права и даем разрешение на три команды:


![image](https://github.com/user-attachments/assets/110927dc-1923-49d6-bc58-ab1174003ce8)


Пользователь у пользователя появилась возможность пользоваться только выделенными командами:


![image](https://github.com/user-attachments/assets/c971c94d-7485-4019-82fe-5eea020b656b)









