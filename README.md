Turgon Configuration
====================================

We've got a nice media center setup. Sickbeard, SabNZBd, Couchpotato,
Maraschino, and XBMC all run behind an nginx reverse proxy. This gives us
access to our media from anywhere.

Beyond simply installing those programs, here is what we have done to make
everything work together:

Generate an htpasswd file
---------------------------
```bash
USERNAME=[your username here]
PASSWORD=[your password here]

# as root
SALT=$(echo -n $RANDOM$RANDOM$RANDOM | openssl sha1 -binary)
DIGEST=$(echo -n $PASSWORD$SALT | openssl sha1 -binary)
echo $USERNAME':{SSHA}'$(echo -n $DIGEST$SALT | base64) > /etc/nginx/htpasswd
chown nginx:nginx /etc/nginx/htpasswd
chmod 600 /etc/nginx/htpasswd
```

Apply patches to the open source stuff
--------------------------
cd /opt/sickbeard
git am ~/path/to/turgon-config/sickbeard.patch

cd /opt/maraschino
git am ~/path/to/turgon-config/maraschino.patch

Probably more stuff?
-------------------------
If anyone somehow finds this, let me know how it goes for you.
