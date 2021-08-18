# ssh-key-generating

## 1. Генерируем новый (или первый) свой ключ SSH в консоли Git Bash или в терминале MacOS 
командой, указав свой email, привязаный к учетной записи Git Hub     
```ssh-keygen -t ed25519 -C "your_email@example.com"```  
В консоли появится вопрос:   
```
Enter a file in which to save the key (/Users/you/.ssh/id_ed25519): [Press enter]
``` 
- нажмите Enter  
Далее появится:
```
Enter passphrase (empty for no passphrase): [Type a passphrase]
``` 
- придумайте и впишите кодовое слово,
потом появится запрос о подтверждении введенного выше кодового слова:   
```
Enter same passphrase again: [Type passphrase again]
``` 
- повторите ввод своего кодового слова.   
Ответ консоли (терминала) примерно следующий:
```
Your identification has been saved in /c/Users/lenovo/.ssh/id_ed25519

Your public key has been saved in /c/Users/lenovo/.ssh/id_ed25519.pub

The key fingerprint is:
SHA256:44oMwxVMs7TO1WKHLGNrV/HvxX7+YFCqejxENElyag4 your_email@example.com

The key's randomart image is:
тут схематичная картинка)

```
У вас в корне компьютера появится папка .ssh с файлами ключей
(у меня например расположение такое: C/Windows/Users/lenovo/.ssh)   

## 2. Запускаем ssh-agent для управления ключем SSH, командой в консоли или терминале  
```eval "$(ssh-agent -s)"```  
В ответ на введенную команду вы увидите id вашего запущенного агента, как на примере ниже:  
```
Agent pid 2158
```
- на MacOS нужно еще создать файл, командой    
```touch ~/.ssh/config```   
открыть этот файл в редакторе кода и вставить в него следующий код:
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```
## 3. Теперь добавляем в запущенный ssh-agent, сгенерированный ключ SSH,командой:  
```ssh-add ~/.ssh/id_ed25519```  
Вас попросят ввести ваше кодовое слово. 
После его ввода появится ответ консоли: 
```
Identity added: /c/Users/lenovo/.ssh/id_ed25519 (your_email@example.com)
```
## 4. Теперь нужно сохранить ваш новый ключ в учетной записи Git Hub:
- расположение в профиле   
```profile/settings/SSH and GPG keys/```   
- в открывшейся странице в разделе ```SSH keys``` нажимаем зеленую кнопку ```New SSH key```   
- указываем заголовок в поле Title, например key, а в поле Key вписываем свой ключ в следующем формате (так, как ответила консоль при генерации ключа, п.1 The key fingerprint is):
```
SHA256:44oMwxVMs7TO1WKHLGNrV/HvxX7+YFCqejxENElyag4 your_email@example.com
```
- ключ сохранен.

## 5. Теперь вам следует заново склонировать репозиторий с Git Hub, указывая при клоне ссылку через SSH (!!!НЕЛЬЗЯ HTTPS!!!)

## 6. В слонированный заново репозиторий через SSH перенесите внимательно файлі с кодом, <b>исключая</b> перенос папки <b>.git</b> старого репозитория.

## 7. В новосклонированном репозитории можно делать команды 
```
git add .
git commit -m "add files by ssh key"
git push
```
и деплой само собой
```
npm run deploy
```
