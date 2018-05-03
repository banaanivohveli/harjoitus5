# Harjoitus 5

## c) Aja oma Salt-tila suoraa git-varastosta.

Aloitin harjoituksen luomalla repositoryn GitHubiin. Tämän jälkeen kopsasin selaimessa linkin repoon, loin palvelimella uuden kansion ja
kloonasin repon Gitillä.

	$ mkdir harjoitus5
	$ git clone https://github.com/banaanivohveli/harjoitus5.git

Hyppäsin kansion sisään, initoin gitin ja aloitin Salt-tilan luomisen. Tehtävää varten tein yksinkertaisen tilan, joka asentaa irssin.

	$ cd harjoitus5
	$ git init
	$ mkdir salt
	$ cd salt
	$ nano irssi.sls

Irssi.sls sisältö:

	$ irssi:
	$   pkg.installed

Tein sille kaveriksi samaan kansioon myös top.sls, johon sijoitin luodun irssi-staten.


Tämän jälkeen palasin juurikansioon, johon loin gitti.sh-skriptin.
Skriptin sisältö:
	
	$ git add . && git commit && git pull && git push

Ideana siis, että yhdellä komennolla voi lisätä kaiken Gittiin, pullata ja pushata. Testaus:
	
	$ bash gitti.sh
