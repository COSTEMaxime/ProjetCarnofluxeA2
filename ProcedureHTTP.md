Proc�dures d'installation du serveur web Apache2
===================

La premi�re �tape est l'installation du service Apache2 :

    apt-get install apache2

L'exemple suivant explique la d�marche pour ajouter le VHost carnofluxe.fr, mais elle peut-�tre utilis�e pour ajouter n'importe quel VHost.

Il faut ensuite cr�er les diff�rents fichiers qui vont contenir les fichiers des diff�rents VHosts. On cr�� d'abord les diff�rents r�pertoires dans le r�pertoire /var/www/. Ce r�pertoire stockera tous nos fichiers html.
On cr�� aussi un fichier index.html qui sera la page d�accueil de notre site.

    mkdir /var/www/carnofluxe.fr/
    nano /var/www/carnofluxe.fr/index.html

Il faut ensuite remplir le fichier index.html pour qu'il puisse afficher une page web :

    <html>
		<head>
			<title>Carnofluxe - Accueil</title>
		</head>
		
		<body>
			<h1>Site Carnofluxe.fr</h1>
		</body>
	</html>
Il faut ensuite cr�er le fichier de configuration qui va contenir les param�tres du VHost :

    <VirtualHost carnofluxe.fr:80>
    
	    ServerAdmin mail@test.com
	    ServerName carnofluxe.fr
	    ServerAlias www.carnofluxe.fr
	    
		DocumentRoot /var/www/carnofluxe.fr/
			DirectoryIndex index.html
			
		<Directory /var/www/carnofluxe.fr/>
			Require all granted
			AllowOverride All
		</Directory>

	ErrorLog /var/log/apache2/error.log
	CustomLog /var/log/apache2/access.log combined
	
	</VirtualHost>


Ensuite il faut rendre les sites accessibles en utilisant la commande suivante :

    a2ensite carnofluxe.fr

