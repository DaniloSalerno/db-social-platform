# Seleziona tutti gli utenti e calcolane l'età (25)
```SQL
SELECT `id`,`username`, FLOOR(DATEDIFF(CURDATE() , `birthdate`) / 365) AS `age` FROM `users`;
```

# Seleziona tutti i post senza Like (13)
```SQL
SELECT `posts`.* FROM `posts` LEFT JOIN `likes` ON `posts`.`id` = `likes`.`post_id` WHERE `likes`.`post_id` IS NULL;
```

# Conta il numero di like per ogni post (165)
```SQL
SELECT `posts`.`id`, `posts`.`title`, COUNT(`likes`.`post_id`) AS `likes_number` FROM `posts` LEFT JOIN `likes` ON `posts`.`id` = `likes`.`post_id` GROUP BY `posts`.`id`;
```

# Ordina gli utenti per il numero di media caricati (25)
```SQL
SELECT `user_id`, COUNT(`user_id`) AS `media_count` FROM `medias` GROUP BY `user_id` ORDER BY `media_count` DESC;
```

# Ordina gli utenti per totale di likes ricevuti nei loro posts (25)
```SQL
SELECT `user_id`, COUNT(`post_id`) AS `likes_number` FROM `likes` GROUP BY `user_id` ORDER BY `likes_number` DESC;
```

# Seleziona tutti i post degli utenti tra i 20 e i 30 anni (49)
```SQL
SELECT `posts`.* FROM `posts` JOIN `users` ON `posts`.`user_id` = `users`.`id` WHERE FLOOR(DATEDIFF(CURDATE() , `users`.`birthdate`) / 365) BETWEEN 20 AND 30;
```

# Seleziona il numero di post e di media per ogni utente (25)
```SQL
SELECT `users`.`id` AS `user_id`, COUNT(DISTINCT `posts`.`id`) as `posts_count`, COUNT( DISTINCT`medias`.`id`) as `medias_count` FROM `users` JOIN `posts` ON `users`.`id` = `posts`.`user_id` JOIN `medias` ON `users`.`id` = `medias`.`user_id` GROUP BY `users`.`id`;
```


## BONUS
# Seleziona tutti i post che contengono il tag 'serata' (8)
```SQL
SELECT * FROM `posts` WHERE JSON_CONTAINS(`tags`, '["serata"]');
```

# Ordina i post in base al numero di tag (165)
```SQL
SELECT *, JSON_LENGTH(`tags`) AS `tag_count` FROM `posts` ORDER BY `tag_count` DESC ,`id`;

```

# Ordina gli utenti in base al numero di tag usati nei loro post (25)
```SQL
SELECT `users`.*, SUM( JSON_LENGTH(`posts`.`tags`)) AS `tag_count` FROM `users` JOIN `posts` ON `users`.`id` = `posts`.`user_id` GROUP BY `users`.`id` ORDER BY `tag_count` DESC, `users`.`id`;
```
