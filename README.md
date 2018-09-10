# pagemetrics
A demo site for testing various page metrics scripts


## 1. Using Matomo

Website [link](https://matomo.org).

### Prerequisites (Minimum system requirements)

- Webserver such as Apache, Nginx, IIS, etc.
- PHP version 5.5.9 or greater
- MySQL version 5.5 or greater, or MariaDB
- (enabled by default) PHP extension pdo and pdo_mysql, or the mysqli extension.

#### Recommended Configuration

- PHP 7 (more memory efficient and faster than previous PHP versions)
- MySQL 5.7+ or MariaDB for database
- few extra PHP extensions: PHP GD extension
	
	```
	$ sudo apt-get install php7.0 php7.0-curl php7.0-gd php7.0-cli mysql-server php7.0-mysql php-xml php7.0-mbstring
	```

## Installation

1. Download the **self-hosted Matomo** source codes from [here](https://matomo.org/download/). A mirror download as of this writing, version 3.6.0 is available [here]().
2. Extract the contents into your webserver, example: `http://localhost/analytics`.
3. Run the website to initialize your first website url to track by loading `http://localhost/analytics`.


### First-time Matomo Installation (Initialization)

#### 1. Database Set-up

1. Login to PhpMyAdmin
2. Create a database that you will use for Matomo
3. Create a database user with a password

#### 2. Notes:

- Fill in the required fields (some of them may need to get details from your MySQL database).

- If you run into an error ` Matomo reports this error and doesn’t continue: “Fatal error: Maximum execution time of 30 seconds exceeded in …`, change your `php.ini`'s `max_execution_time=30` to `0` and try again.

#### 3.  Methods - Default Website Initialization Set-up

1. **Welcome**<br>
Welcome introductory page.

2. **System Check**<br>
This page checks if your system requirements are met by your machine.

3. **Database Setup**<br>
	- Database Server: 127.0.0.1 / localhost
	- Login: <YOUR_DB_USERNAME>
	- Password: <YOUR_DB_USER_PASSWORD>
	- Database Name: <YOUR_DATABASE_NAME>
	- Table Prefix: (Leave as ease or change)
	- Adapter: PDO\MYSQL

4. **Super User**<br>
	- Super user login: (create a random super user login name)
	- Password: Create a password
	- Password (repeat): repeat password
	- Email: enter a valid email

5. **Setup a Website**<br>
	- Website name: Enter your website-to-track's name
	- Website URL: Enter your website-to-track's URL
	- Website time zone: Enter your country
	- Ecommerce: Select *Not an Ecommerce site*

6. **Javascript Tracking Code**<br>
	- Copy the printed JavaScript Tracking Code, paste between website's `<head></head>` tag.

7. **Congratulations**
	- congrats! First website tracking code and set-up is finished
	- Press *Continue to Matomo* button

#### 4. Grant View Access to Anonymous User

An *Anonymous user* will be used to view your account's data publicly without logging into your Matomo instance.

1. Go to Administration (gear icon on upper right) > System > Users
2. Set *anonymous* user's *Role for <website_name>* to *View*
3. Go to Administration > Anonymous user > Anonymous user settings
	- *Dashboard for a specific website* = Offline Website
	- *For anonymous users, report date to load by default* = Las 7 days (including today)
4. Set the not logged-in view for anonymous users
	- Go to System > Anonymous user
	- Inside the *Anonymous user settings* set: 
		- **When users are not logged in and visit Matomo, they should access** = The login screen

#### 5. Install Plugins

1. **GeoLocation**
	- Go to Administration (gear icon on upper right) > System > Geolocation
	- Download the *GeoIP 2 (Apache)* free databases from the following links. *City* is recommended to be used.
		- **GeoLite2 City** - [binary](http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz) | [csv](http://geolite.maxmind.com/download/geoip/database/GeoLite2-City-CSV.zip) | [mirror all format]()
		- **GeoLite2 Country** - [binary](http://geolite.maxmind.com/download/geoip/database/GeoLite2-Country.tar.gz) | [csv](http://geolite.maxmind.com/download/geoip/database/GeoLite2-Country-CSV.zip) | [mirror all format]()
		- **GeoLite2 ASN** - [binary](http://geolite.maxmind.com/download/geoip/database/GeoLite2-ASN.tar.gz) | [csv](http://geolite.maxmind.com/download/geoip/database/GeoLite2-ASN-CSV.zip) | [mirror all format]()
	- Extract the content of *GeoLite2-City_20180905.tar*. Copy the extracted *GeoLite2-City.mmdb* into `/PATH_TO_MATOMO/misc/`
	- Refresh the browser page, then press **Save**.

2. **Use SSL (https) - ForceSSL**
	- Forces to serve data and content over SSL
	- Download and install the ForceSSL plugin from [here](http://plugins.matomo.org/ForceSsl) or mirror link [here](). Extract contents to `<PATH_TO_MATOMO>/plugins/ForceSSL`
	- Alternatively, you can edit your `config/config.ini.php` / `global.ini.php` file and add under the `[General]` section, set the following:
	
			[General]
			force_ssl = 1
	- for more information, read complete instructions from [here](https://matomo.org/faq/how-to/faq_91/).

#### 6. Allow CORS
- Open `config/global.ini.php`
- Edit the following lines: 
	
			[General]
			cors_domains[] = *
- to allow CORS only on specific websites
	
			[General]
			cors_domains[] = "http://example.com"
			cors_domains[] = "http://dashboard.example.com"



### 7. Adding a New Website to Track

The following script will track a webpage when embedded between the `<head></head>` part.

1. Login using your created user credentials during first-time initialization to your hosted Matomo at `http://localhost/analytics`
2. Click the Administration link (gear icon) on the upper right topbar menu.
3. Navigate to the sidebar. 
	- Go to Websites > Manage 
4. Press the Add a New Website button
5. Fill in the input fields, answering only the input fields from the default website initialization. Other input fields may be explored later.


### 8. Embed a Tracking Script to a Website 	

The following script will track a webpage when embedded between the `<head></head>` part.

1. Login using your created user credentials during first-time initialization to your hosted Matomo at `http://localhost/analytics`
2. Click the Administration link (gear icon) on the upper right topbar menu.
3. Navigate to the sidebar. 
	- Go to Websites > Manage 
4. Select a website row, then click *View Tracking Code*
5. Scroll down and copy the script under *JavaScript Tracking Code* into the `<head></head>` part of your website.



### 9. Embed an Analytics Widget to your Website

1. Go to Administration (gear icon on upper right) > Platform > Widgets
2. Go to Widgetize reports
	- Select Visitors > Visitors Overview (with Graph)
3. Copy the `Embed iframe`  or `direct link` codes into your website.
4. (OPTIONAL) Disable Annotations for anonymous users
	- Go to Administration > System > Plugins
	- Find the *Annotations* plugin and disable it

----------

