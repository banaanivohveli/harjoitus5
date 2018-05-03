# Harjoitus 5

## c) Aja oma Salt-tila suoraa git-varastosta.

Aloitin harjoituksen luomalla repositoryn GitHubiin. Tämän jälkeen kopsasin selaimessa linkin repoon, loin palvelimella uuden kansion ja
kloonasin repon Gitillä.

	mkdir harjoitus5
	git clone https://github.com/banaanivohveli/harjoitus5.git

Hyppäsin kansion sisään, initoin gitin ja aloitin Salt-tilan luomisen. Tehtävää varten tein yksinkertaisen tilan, joka asentaa irssin.

	cd harjoitus5
	git init
	mkdir salt
	cd salt
	nano irssi.sls

Irssi.sls sisältö:

	irssi:
	  pkg.installed

Tein sille kaveriksi samaan kansioon myös top.sls-tiedoston, johon sijoitin luodun irssi-staten.


Tämän jälkeen palasin juurikansioon, johon loin gitti.sh-skriptin.
Skriptin sisältö:
	
	git add . && git commit && git pull && git push

Ideana siis, että yhdellä komennolla voi lisätä kaiken Gittiin, pullata ja pushata. Testaus:
	
	bash gitti.sh

Tekstiä vilisee, git pyytää antamaan commitin editointitekstin, pyytää salasanan ja siirtää kaiken GitHubiin. Toimi hyvin!

Tämän jälkeen loin vielä woop.sh-skriptin, joka ajaisi highstaten, eli tässä tapauksessa asentaisi irssin, jos sitä ei ole aiemmin asennettu. 
woop.sh sisältö:

	sudo salt-call --local state.highstate --file-root salt/

Testataan koko jutun toiminta!

	rm -rf harjoitus5
	git clone https://github.com/banaanivohveli/harjoitus5.git
	cd harjoitus5
	bash woop.sh

Nätisti toimi!

	[INFO    ] Completed state [irssi] at time 20:45:20.869449
	local:
	----------
	ID: irssi
	Function: pkg.installed
	Result: True
	Comment: Package irssi is already installed
	Started: 20:45:18.628790
	Duration: 2240.659 ms
	Changes:

	Summary for local
	------------
	Succeeded: 1
	Failed:    0
	------------
	Total states run:     1

