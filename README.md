### 🔥 Fixing Issue of Connection acquisition timed out
```console
Neo4jError: Connection acquisition timed out in 60000 ms. 
Poos status: Active conn count = 100, Idle conn count = 0.
```

There is also a [open pull request](https://github.com/adam-cowley/nest-neo4j/pull/5) in merging queue. you can install pacakge using github till merge and package publish. see Installation section bellow.



<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://kamilmysliwiec.com/public/nest-logo.png#1" alt="Nest Logo" />   </a>
  <a href="https://neo4j.com" target="_blank"><img src="https://dist.neo4j.com/wp-content/uploads/20140926224303/neo4j_logo-facebook.png" width="380"></a>
</p>

# Nest Neo4j

> Neo4j integration for Nest

## Description

This repository provides [Neo4j](https://www.neo4j.com) integration for [Nest](http://nestjs.com/).

## Installation

```bash
# Npm
$ npm i --save amirHossein-Ebrahimi/nest-neo4j
# Yarn
$ yarn add amirHossein-Ebrahimi/nest-neo4j
```

## Quick Start

Register the Neo4j Module in your application using the `forRoot` method, passing the neo4j connection information as an object:

```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { Neo4jModule } from 'nest-neo4j';

@Module({
  imports: [
    Neo4jModule.forRoot({
      scheme: 'neo4j',
      host: 'localhost',
      port: 7687,
      username: 'neo4j',
      password: 'neo',
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

## Querying Neo4j

The `Neo4jService` is `@Injectable`, so can be passed into any constructor:

```ts
import { Neo4jService } from 'nest-neo4j';

@Controller()
export class AppController {
  constructor(
    private readonly appService: AppService,
    private readonly neo4jService: Neo4jService,
  ) {}

  @Get()
  async getHello(): Promise<any> {
    const res = await this.neo4jService.read(
      `MATCH (n) RETURN count(n) AS count`,
    );

    return `There are ${res.records[0].get('count')} nodes in the database`;
  }
}
```

## Methods

```ts
getConfig(): Neo4jConfig;
getReadSession(database?: string): Session;
getWriteSession(database?: string): Session;
read(query: string, params?: object, database?: string): Result;
write(query: string, params?: object, database?: string): Result;
```
