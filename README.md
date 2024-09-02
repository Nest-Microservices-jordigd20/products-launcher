# Products launcher

This repository contains all the source code from all the microservices that are part of the application.
Each microservice has its own repository, but I am using git submodules to manage them all in one place.

This is the first time I am using microservices so part of the code is based on this [NestJS + Microservices](https://www.udemy.com/course/nestjs-microservicios/?kw=nestjs+microservicios&src=sac) course.

## Key Components

- [API Gateway](https://github.com/Nest-Microservices-jordigd20/client-gateway/tree/master) - Acts as the entry point of the application, it routes the requests to the corresponding microservice and it is responsible for the validation of the requests.
- [Auth Microservice](https://github.com/Nest-Microservices-jordigd20/auth-ms/tree/main) - Manages the authentication and authorization of the users making use of JWT tokens. It also manages the users using MongoDB as the database.
- [Products Microservice](https://github.com/Nest-Microservices-jordigd20/products-ms/tree/master) - Manages the products of the application, allowing the users to create, update, delete and list the products. It uses SQLite as the database.
- [Orders Microservice](https://github.com/Nest-Microservices-jordigd20/orders-ms/tree/master) - This service is responsible for creating the orders and manage their status. It uses PostgreSQL as the database.
- [Payments Microservice](https://github.com/Nest-Microservices-jordigd20/payments-ms/tree/master) - Manages the payments of the application, using Stripe as the payment gateway. This service is hybrid, it has one REST endpoint that is used.


## Technologies

- **NestJS**: Node.js framework used for building for building efficient, reliable and scalable server-side applications.
- **Nats**: Message broker used for the communication between the microservices.
- **Docker**: For containerizing the services, facilitating deployment in any environment in a consistent and reproducible way.
- **PostgreSQL**: Relational database selected for its reliability and ability to handle large volumes of data.
- **MongoDB**: NoSQL database used for the users in the auth microservice.
- **Stripe**: Payment gateway used for the payments microservice.
- **Prisma**: ORM used in OrdersMS, AuthMS and ProductsMS.

## Architecture

The architecture of the application is based on the microservices architecture pattern. Each microservice is a separate entity that is responsible for a specific part of the application. The communication between the microservices and the API Gateway is done using the NATS message broker.

All the services are containerized using Docker, which allows them to be encapsulated in a private network allowing only the necessary services to be exposed to the outside. The only services exposed to the outside are the API Gateway and the webhook endpoint of the Payments Microservice.

<img src="https://res.cloudinary.com/demz9lbb3/image/upload/v1725293236/products-microservices/pevwowr0fl9pzrhgqd0w.webp" alt="System Architecture"/>

## Development environment

1. Clonate the repository
2. Install the dependencies
3. (Optional) If it's the first time you clone the repository run the following command to rebuild the submodules

```bash
git submodule update --init --recursive
```

4. Create a `.env` based on the `.env.template` file.
5. Run the following command:

```bash
$ docker compose up --build
```


## Production environment

1. Clonate the repository
2. Creat a `.env` file based on the `.env.template` file.
3. (Optional) If it's the first time you clone the repository run the following command to rebuild the submodules

```bash
git submodule update --init --recursive
```
4. Run the following command:

```bash
$ docker compose -f docker-compose.prod.yml build
```

## Git Submodules

1. To add a submodule, run the following command, where `<repository_url>` is the URL of the repository you want to add and `<directory_name>` is the name of the directory where the repository will be cloned. (The directory must not exist)

```bash
git submodule add <repository_url> <directory_name>
```

2. Add the changes to the repository

```bash
git add .
git commit -m "Add <directory_name> submodule"
git push
```

3. When someone clones the repository for the first time, they will have to run the following command to initialize and update the submodules

```bash
git submodule update --init --recursive
```

4. To update the submodules references

```bash
git submodule update --remote
```

### Important

If you are working in the submodule repository, you should first **update and push** the changes in the submodule and **then** update the changes in the main repository.

If you do it the other way around, you will lose the references of the submodules in the main repository and you will have to resolve conflicts.
