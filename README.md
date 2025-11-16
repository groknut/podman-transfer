
## Перенос контейнера на другой компьютер

Рассматриваемый образ: [Практикум Docker - создание веб-приложения в контейнере](https://github.com/groknut/bottle-app-docker)

Как известно, нередко программное обеспечение распространяется в виде образов Docker. 

Мы выполним перенос образа с одной системы на другой компьютер. Для этого выполните следующие действия:

### Получите образ из контейнера (commit)
```bash
podman commit -a groknut bottle-docker-app
```
![Коммит](./assets/commit.png)
### Выгрузите образ в файл (save)
```bash
podman save -o bottle-app-docker.tar localhost/bottle-app-docker
```
![Коммит](./assets/save.png)
### Заархивируйте файл любимым архиватором и передайте файл на другой компьютер
```PowerShell
Compress-Archive -Path .\bottle-app-docker.tar -DestinationPath .\bottle-app-docker.zip
```
![Коммит](./assets/zip.png)
### Извлеките файл с образом из архива
```bash
unzip bottle-app-docker.zip
```
![Разархивирование](./assets/unzip.png)
### Загрузите образ в Podman (load)
```bash
podman load -i bottle-app-docker.tar
```
![Загрузка](./assets/load.png)
### Запустите контейнер на основе полученного образа
```bash
podman -d -p 5000:5000 --name bottle-app localhost/bottle-app-docker
```
![Запуск](./assets/run.png)

<div align="center">
<img src="./assets/screen-site-record.gif" alt="Работа сайта (gif)">
</div>
