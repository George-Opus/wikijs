# Mon TEST
**Voici le meilleur tuto ever**

> Et oui cree par moi!!!!

1. frf
2. rffr
3. frrfs
* fzer
* fef
* edezdze




```sh
#!/bin/bash

verif=$(ps aux | awk '/server.py/ {print $11,$12}' | head -n1)
test='python3 server.py'

if [ "$verif" != "$test" ]
then
	echo prout
fi

```
