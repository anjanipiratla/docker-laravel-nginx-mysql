# docker-laravel-nginx-mysql
Dockerizing a laravel application with nginx as web server and mysql as database with persistent volume.

- Create docker-compose.yml file. Divide the file into required sections or blocks such as server, php and mysql. Add volumes to each section so all code base resides at same place i.e. /var/www/html. Also add volume for mysql data to persist under mysql block and main volumes block. 
- Creating laravel project in src folder: Run this command 'docker compose run create-project laravel/laravel .'
- Starting services or containers: Run this command 'docker compose up -d server'.
- Migrate data: Once all the three containers php, mysql and nginx are running, make sure to run this command to populate data 'docker compose run artisan migrate'.
- To bring down all the services: Run this command 'docker compose down'. If you want to remove volume as well 'docker compose down -v'.

Challenges faced:
- Initially mysql volumes were anonymous, then I realized that they will be gone once I bring down the containers. Then I had added volumes to mysql section and to the main section of docker-compose.yml. When you add volumes like this then you will have a named volume so that you can easily identify which volume you are using for your mysql data.
- Also whenever you make any changes to the code, the changes were not getting reflected in containers. Figured out that you need to bring down all continers and then run this command 'docker compose run -d --build server' which will reflect all your changes in code to the containers.