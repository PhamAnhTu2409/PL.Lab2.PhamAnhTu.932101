# Лабораторная работа 1 — Wget на минималках

**СТУДЕНТ**: Фам Ань Ту  
**ГРУППА**: 932101  

# REQUIRES:

## Структура:

1. manifest.json, service-worker.js, icons 
2. index.html (scipt: client.js)

## Install WPA:

1. Button Install (will be hidden if app is installed, handled by beforeInstallPrompt Event) 
2. Run offline with caches 

## Using storage:

1. IndexedDB 

## Data and operations:

1. Create Domain 
2. Delete Domain (with all profiles inside domain) 
3. Create Profile (with auto generated password) 
4. Edit Profile Password 
5. Show Info Profile Password (with old passwords before edited) 
6. Delete Profile 



# RESULT:

- Запустить программу с коммандой "npx serve .", чтобы Service Worker смог работать, или просто открыть файл index.html на браузере (но будет без функции INSTALL)

- Приложение нужен интернет, потому что он использует "cdn tailwindcss" для стиля и "google font". По требованию это можно решать способом установить tailwindcss в папке проекта

- Обяснение файла scipt client.js: Он дает класс PasswordManagerApplication, который обеспечивает все методы, работающие с IndexedDB. Method displayList() отображает список домейнов и профилов на index.html строкой JSX. Каждый раз displayList() зовут, программа делает (document.removeEventListener) и заново (document.addEventListener), чтобы старые поведения не влияет на работу приложения.

- IndexedDB сохраняет 2 таблицы (ObjectStore): domains, profiles. Структура:

`domains {id:number(auto increment), name:string (unique)}`

`profiles {id:number(auto increment), username:string, password:string, oldPassword[{password:string, savedAt:timestamp}], updatedAt:timestamp}`
