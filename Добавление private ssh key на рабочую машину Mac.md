Если имеется сгенерированный ssh приватный ключ, то необходимо добавить его в цепочку ключей:

1. Создаем файл для ключа (например id_rsa_private) и копируем в него ключ.
2. Применяем к нему права для пользователя  `chmod 600 id_rsa_private`.
3. Добавляем в цепочку паролей ssh `ssh-add -K  id_rsa_private`.
4. Открываем файл ~/ssh/config и в него прописываем  
        Host*  
                SendEnv LANG LC_*  
                UseKeychain yes  
                AddKeysToAgent yes  
                IdentityFile /Users/pavel.agarkov/Desktop/ssh/id_rsa  
