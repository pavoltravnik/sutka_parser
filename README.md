# sutka_parser


Statistics is accessible on (https://pavoltravnik.github.io/sutka_parser/)[https://pavoltravnik.github.io/sutka_parser/]


create file sutka.sh
```
site="$(curl -s  https://www.sutka.eu/)"
obsazenost="$(echo $site | grep -o -P '(?<=<strong>)[0-9]*?(?=%<\/strong>\sobsazenost:)')"
bazen="$(echo $site | grep -o -P '(?<=<strong>)[0-9]*?(?=<\/strong>\s*\(Baz)')"
aquapark="$(echo $site | grep -o -P '(?<=<strong>)[0-9]*?(?=<\/strong>\s*\(Aquapark\))')"


# Post data to firebase
curl -X POST -d '{ "obsazenost": '$obsazenost' , "bazen": '$bazen', "aquapark": '$aquapark', "timestamp": '"$(date +%s)"' }' \
  'https://[DB-NAME].firebaseio.com/users/obsazenost.json?auth=[AUTH-KEY]'
```

edit crontab

```
0,10,20,30,40,50 * * * * /<path to file>/sutka.sh
```