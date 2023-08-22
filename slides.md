---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## NestJSに入門してみよう

drawings:
  persist: false
transition: slide-left
title: さわって学ぶNestJS
---

# NestJSに入門してみよう

2023/08/23 naoki.haba

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

# 自己紹介

- 名前: 羽馬 直樹
- Twitter: <span class="ml-2 text-[#1d9bf0] font-bold">@NaokiHaba</span>
- GitHub: <span class="ml-2 text-[#1d9bf0] font-bold">@NaokiHaba</span>
- 趣味
  - 猫と遊ぶこと
  - ドライブ
  - おでかけ
  - 技術ブログ書いたり登壇したり
  - 登山 etc...

---
layout: center
---

# Topics


1. NestJSとは
2. NestJSの特徴
3. NestJSのインストール
4. NestJSでAPIを作ってみる


---
layout: iframe-right
url: https://nestjs.com/
---

# NestJSとは

- `Node.js`のフレームワークのひとつ
- `TypeScript`で構築されている
- `GraphQL`やマイクロサービスなど、さまざまな機能をサポート
- `Angular`や`React`など、さまざまなフロントエンドフレームワークと連携が可能
- テストツールに依存せず、[Jest](https://github.com/facebook/jest)や[SuperTest](https://github.com/ladjs/supertest)との統合が容易
- [NestJS Japan Users Group](https://nest-jp.connpass.com/)が運営されている

---
layout: image-right
image: images/diagram.png
---

## 全体像

NestJSのファイル構成と、利用されるコアファイルを説明します。

まず、ファイル構成は次のようになっています。

```
src/
├── app.controller.ts # アプリケーションのルートに対するリクエストを処理する
├── app.module.ts # アプリケーションのルートモジュール
├── app.service.ts # アプリケーションのルートに対するリクエストを処理する
├──  main.ts # アプリケーションのエントリポイント
```

それぞれの階層との関係は右図の通りです。

---
layout: center
---

## デコレータ：NestJSの便利な機能

NestJSでは、`@`から始まるデコレータを利用することで、様々な機能を実現しています。

例えば次のようなデコレータが、NestJSには用意されています。

| デコレータ      | 役割 |
|-----------------|------|
| `@Controller()` | コントローラを定義する |
| `@Get()`        | GETリクエストを処理する |
| `@Post()`       | POSTリクエストを処理する |
| `@Put()`        | PUTリクエストを処理する |
| `@Delete()`     | DELETEリクエストを処理する |
| `@Patch()`      | PATCHリクエストを処理する |

---
layout: center
---

## 依存性注入（DI）

**依存性注入**<small>（DI、Dependency Injection）</small>とは、クラスの依存関係を解決する仕組みです。NestJSでは、依存性注入を使ってクラスの依存関係を解決します。

```typescript

@Injectable()

class A {
  constructor() {}
}
```


そして、次のようなクラスBがあったとします。このクラスは、`@Inject()`デコレータを使って依存性を注入しており、クラスAに依存しています。

```typescript

@Injectable()

class B {
  constructor(@Inject(A) private a: A) {}
}
```

---
layout: center
---

## NestJS CLI

NestJSには、CLIツールが用意されています。CLIツールとは、コマンドラインからアプリケーションを作成したりテストを実行したりするツールのことです。

NestJS CLIを使うことで、次のようにさまざまなことが実行できます。

- アプリケーションの作成
- モジュールの作成
- コントローラの作成
- サービスの作成
- テストの実行
- ビルド

---
layout: center
---

# NestJSのインストール

ここからは、NestJSのインストールを行っていきます。

時間の都合上、今回は以下のリポジトリを使って作業を進めていきましょう。

https://github.com/NaokiHaba/nestjs-example2

---
layout: center
---

## NestJS CLIで環境構築を行う

このセクションでは、NestJSの環境構築を行っていきます。次の2つの方法があります。

- NestJS CLIを使う
- 手動で環境構築する

今回はNestJS CLIを使います。まず次のコマンドを実行して、NestJS CLIそのものをインストールします。

```sh
$ npm i -g @nestjs/cli
```

その後、次のコマンドを実行して、NestJSのプロジェクトを作成します。

```shell
$ nest new nestjs-example2

# 作成完了後、次のようなメッセージが表示されます。
Which package manager would you ❤️  to use? npm
✔ Installation in progress... ☕

🚀  Successfully created project nestjs-example
👉  Get started with the following commands:

$ cd nestjs-example2
$ npm run start
```

---
layout: center
---

## ローカル環境で動作確認を行う

作成したディレクトリに移動して、次のコマンドでアプリケーションを起動しましょう。

```sh
$ cd nestjs-example2
$ npm run start:dev

# 起動完了後、次のようなメッセージが表示されます。
[Nest] 13473  - 08/23/2023, 3:09:23 AM     LOG [NestFactory] Starting Nest application...
[Nest] 13473  - 08/23/2023, 3:09:24 AM     LOG [InstanceLoader] AppModule dependencies initialized +102ms
[Nest] 13473  - 08/23/2023, 3:09:24 AM     LOG [RoutesResolver] AppController {/}: +12ms
[Nest] 13473  - 08/23/2023, 3:09:24 AM     LOG [RouterExplorer] Mapped {/, GET} route +3ms
[Nest] 13473  - 08/23/2023, 3:09:24 AM     LOG [NestApplication] Nest application successfully started +3ms
```

この状態で`http://localhost:3000`にアクセスすると、 `Hello World!` と表示されます。

---
layout: center
---

## MySQLコンテナを起動する

`docker-compose.yml`の定義については割愛します。詳細は、リポジトリの`docker-compose.yml`を参照してください。

次のコマンドを実行してMySQLコンテナを起動します。

```sh
$ docker-compose up -d
```

---
layout: iframe-right
url: https://typeorm.io/
---

## TypeORMのセットアップ

起動したMySQLに接続するため、ORマッパーとして**TypeORM**を利用します

次のコマンドを実行して、TypeORMをインストールします。TypeORMをインストールすると、`typeorm`コマンドが使えるようになります。

```sh
$ npm install --save @nestjs/typeorm typeorm mysql2
```

---
layout: center
---

続いてTypeORMの設定ファイルを作成します。`typeOrm.config.ts`という名前でファイルを作成し、次のように記述します。

```typescript
import { DataSource } from 'typeorm';

export default new DataSource({
  type: 'mysql',
  host: 'localhost',
  port: 3306,
  database: 'test',
  username: 'test',
  password: 'password',
  entities: ['dist/**/entities/**/*.entity.js'],
  migrations: ['dist/**/migrations/**/*.js'],

  // ログを出力するかどうか
  logging: true,

  // synchronize は開発時にのみ使用する
  // trueにすると、エンティティの変更を検知して、自動的にテーブルが更新される
  // 本番環境では、falseにすること
});
```

---
layout: center
---

## 環境変数の設定

データベースに接続するために必要な情報は、環境変数でアプリケーションに渡します。NestJSで環境変数を取得するライブラリとして、`@nestjs/config`を使用します。

次のコマンドを実行してインストールしましょう。

```sh
$ npm install --save @nestjs/config
```


次に、このライブラリの設定ファイルである`config/configuration.ts`を作成します。今回は、次のような内容になります。

```typescript
export default () => ({
  database: {
    host: process.env.DATABASE_HOST || 'localhost',
    port: parseInt(process.env.DATABASE_PORT, 10) || 3306,
    username: process.env.DATABASE_USER || 'test',
    password: process.env.password || 'password',
    name: process.env.database || 'test',
  },
});
```

---
layout: center
---

以上がNestJSの環境構築の手順でした。次のセクションからは、実際にAPIを作成していきます。

- [TypeORM](https://typeorm.io/#/)
- [TypeORMの設定](https://docs.nestjs.com/techniques/database)
- [環境変数の設定](https://docs.nestjs.com/techniques/configuration)

余談ですが、今回はORMとしてTypeORMを使用しましたが、最近は[Prisma](https://www.prisma.io/)を利用する開発者が増えている印象です。Prismaはデータベースから自動でスキーマを生成してくれるので、開発者はスキーマの定義に集中できます。TypeORMは、スキーマの定義を開発者が行う必要があります。

---
layout: center
---

## REST APIの作成

いよいよNestJSでREST APIを作成していきます。今回は、データベース上のユーザー情報を操作する次のようなAPIを作成します。

| メソッド | URL        | 説明 |
|----------|------------|-----------|
| GET      | /users/:id | ユーザーを取得 |
| POST     | /users     | ユーザーを作成 |

---
layout: center
---

## CRUD処理のひな形を作成する

NestJS CLI<small>（`nest`コマンド）</small>を使用することで、リソースに対するCRUD<small>（Create Read Update Delete）</small>処理を次のように簡単に作成できます。

```sh
$ nest g resource users

? What name would you like to use for this resource (plural, e.g., "users")? users
? What transport layer do you use? (Use arrow keys)
❯ REST API
  GraphQL (code first)
  GraphQL (schema first)
  Microservice (non-HTTP)
  WebSockets
? What transport layer do you use? REST API

? Would you like to generate CRUD entry points? Yes

CREATE src/users/users.controller.spec.ts (614 bytes)
CREATE src/users/users.controller.ts (1.02 KB)
CREATE src/users/users.module.ts (1.02 KB)
CREATE src/users/users.service.spec.ts (1.02 KB)
CREATE src/users/users.service.ts (1.02 KB)
CREATE src/users/users.entity.ts (1.02 KB)
CREATE src/users/dto/create-user.dto.ts (1.02 KB)
CREATE src/users/dto/update-user.dto.ts (1.02 KB)
```

---
layout: center
---

ここでは、ユーザーを表す`users`というリソース（`resource`）を作成（`g`enerate）しています。

このコマンドで、以下のようなCRUD処理のひな形となる基本的なファイルが、`nestjs-example2/src/users/`ディレクトリに作成されました。

なお、CLIを使用しなくても同じようなファイルを作成することはできますが、CLIを使用すれば簡単にCRUDを作成できます。


---
layout: center
---

## ユーザー情報を表すエンティティ

まずは、ユーザー情報を表すエンティティを作成します。`users.entity.ts`を次のように編集します。

```typescript
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';

@Entity('users')
export class User {
  @PrimaryGeneratedColumn({
    comment: 'アカウントID',
  })
  readonly id: number;

  @Column('varchar', { comment: 'アカウント名' })
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

---
layout: center
---

このコードでは、TypeORMから次のデコレータをインポートしています。

| デコレータ | 説明 |
|------------|------|
| `@Entity` | データベースのテーブルを定義する |
| `@PrimaryGeneratedColumn` | 主キーを定義する |
| `@Column` | カラムを定義する |

これで定義されるテーブルの構成は、先に説明したような2カラムのシンプルなものです。

なお、TypeORMのデコレータを詳しく知りたい方は公式ドキュメントを参照してください。

▶ [Decorator reference](https://github.com/typeorm/typeorm/blob/master/docs/decorator-reference.md) - typeorm/typeorm

---
layout: center
---

## TypeORMモジュールにエンティティを登録する

先ほど作成したエンティティをTypeORMモジュールに登録し、両者を紐付けます。

`src/users/users.module.ts`を編集します。

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './entities/user.entity';

@Module({
  controllers: [UsersController],
  providers: [UsersService],
  // TypeOrmModule.forFeature()でエンティティを登録する
  imports: [TypeOrmModule.forFeature([User])],
})
export class UsersModule {}
```

---
layout: center
---

## TypeORMモジュールをアプリケーションに登録する

次に`src/app.module.ts`を編集して、TypeORMモジュールをアプリケーションに登録します。

```typescript
@Module({
  imports: [
    TypeOrmModule.forRootAsync({
      imports: [ConfigModule],
      useFactory: async (configService: ConfigService) => ({
        type: 'mysql',
        host: configService.get('database.host'),
        port: configService.get('database.port'),
        username: configService.get('database.username'),
        password: configService.get('database.password'),
        database: configService.get('database.name'),
        entities: ['dist/**/entities/**/*.entity.js'],
      }),
      inject: [ConfigService],
    }),
  ],
})
```

---
layout: center
---

## マイグレーションを実行する

今回はマイグレーションファイルの作成と実行に、TypeORMのCLIツールを使用します。ただし、TypeORMのCLIツールはJavaScriptで書かれているため、今回のようなTypeScriptのファイルには、次のドキュメントに従って[**ts-node**](https://typestrong.org/ts-node/)を使用する必要があります。

また、TypeORMのCLIツールをnpmスクリプトとして実行できるよう、`nestjs-example2`ディレクトリにある`package.json`ファイルに以下の通り追記してください。


```json
{
  "scripts": {
    "typeorm": "ts-node ./node_modules/typeorm/cli",
    "typeorm:run-migrations": "npm run typeorm migration:run -- -d ./typeOrm.config.ts",
    "typeorm:generate-migration": "npm run typeorm -- -d ./typeOrm.config.ts migration:generate ./migrations/$npm_config_name",
    "typeorm:revert-migration": "npm run typeorm -- -d ./typeOrm.config.ts migration:revert"
  }
}
```

---
layout: center
---

### マイグレーションファイルを作成

マイグレーションファイルを作成するには、`typeorm:generate-migration`スクリプトを実行します。

実行前に`dist`ディレクトリを生成しておく必要がありますので、`npm run start:dev`を実行してください。

```sh
$ npm run start:dev
$ npm run typeorm:generate-migration --name=CreateUsers
```

`src/users/users.entity.ts`で定義したテーブルのマイグレーションファイルが、`migrations`ディレクトリに作成されます。


---
layout: center
---

### マイグレーションを実行

作成したマイグレーションファイルを`typeorm:run-migrations`で実行します。

```sh
$ npm run typeorm:run-migrations                       
query: START TRANSACTION

query: CREATE TABLE 
`users` (`id` int NOT NULL AUTO_INCREMENT COMMENT 'アカウントID',
 f`name` varchar(255) NOT NULL COMMENT 'アカウント名', PRIMARY KEY (`id`)) ENGINE=InnoDB

query: INSERT INTO `test`.`migrations`(`timestamp`, `name`) VALUES (?, ?) -- PARAMETERS: [1673728396326,"CreateUsers1673728396326"]
Migration CreateUsers1673728396326 has been  executed successfully.
query: COMMIT
```

これでデータベースにテーブルが作成されました。
以下のコマンドで確認できます。

```sh
$ docker-compose exec db mysql -u root -ppassword -D test -e "DESC users"
mysql: [Warning] Using a password on the command line interface can be insecure.
+-------+--------------+------+-----+---------+----------------+
| Field | Type         | Null | Key | Default | Extra          |
+-------+--------------+------+-----+---------+----------------+
| id    | int          | NO   | PRI | NULL    | auto_increment |
| name  | varchar(255) | NO   |     | NULL    |                |
+-------+--------------+------+-----+---------+----------------+
```

---
layout: center
---

## DTOの作成とバリデーション

続いてDTO<small>（Data Transfer Object）</small>を作成します。
DTOは、データの構造を定義するクラスです。

データ構造をバリデーションするパッケージとして、`class-validator`を使用します。

```sh
$ npm i --save class-validator class-transformer
```

これを使用するように`src/users/create-user.dto.ts`を編集します。

`update-user.dto.ts`もクラス名を除いて同じ内容に編集してください。


```typescript
import { IsNotEmpty, MaxLength } from 'class-validator';

export class CreateUserDto {
  @MaxLength(255)
  @IsNotEmpty()
  name: string;
}
```

---
layout: center
---

## バリデーションの設定

定義したDTOでバリデーションを行うパイプとして`ValidationPipe`を使用するように、`main.ts`で設定します。`useGlobalPipes`でグローバルに設定できます。

```typescript
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
 const app = await NestFactory.create(AppModule);
 app.useGlobalPipes(new ValidationPipe());
 await app.listen(3000);
}
bootstrap();
```

なお、定義できるバリデーションの種類は次のドキュメントを参照してください。

▶ [typestack/class-validator: Decorator-based property validation for classes.](https://github.com/typestack/class-validator)

---
layout: center
---


## ユーザーを作成するAPIの実装

データベースが用意できたので、実際にユーザー情報を操作できるAPIを実装していきましょう。

HTTPリクエストを処理するコントローラは、`src/users/users.controller.ts`に記述します。

```typescript
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Post()
  async create(@Body() createUserDto: CreateUserDto): Promise<User> {
    return await this.usersService.create(createUserDto);
  }
}
```

---
layout: center
---

## サービスにcreateメソッドを追加

次に`src/users/users.service.ts`を編集して、ユーザーを作成するロジックを記述していきます。

```typescript
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User) private userRepository: Repository<User>,
  ) {}

  async create({ name }: CreateUserDto): Promise<User> {
    return await this.userRepository
      .save({
        name: name,
      })
      .catch((e) => {
        throw new InternalServerErrorException(
          `[${e.message}]：ユーザーの登録に失敗しました。`,
        );
      });
  }
}
```

---
layout: center
---

## ユーザーを作成するAPIを実行

いま作成したAPIを実行してみましょう。前述したようにアプリケーションをホットリロードで起動しているため再起動などは必要ありませんが、フロントエンド部分がないためコマンドラインツールでアプリケーションに接続します。

```sh
# ユーザーを作成する
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "test"}' http://localhost:3000/users
{"id":1,"name":"test"} # 戻り値として定義しているUserエンティティが返却される

# nameが空文字の場合は、エラーになる
$ curl -X POST -H "Content-Type: application/json" -d '{"name": ""}' http://localhost:3000/users
{"statusCode":400,"message":"Bad Request","error":"Bad Request"}
```

---
layout: center
---

## ユーザー情報を取得するAPIの実装

次に、ユーザー情報を取得するAPIを実装していきます。

コントローラーにユーザー情報を取得するAPIのリクエストを追加するため、`src/users/users.controller.ts`を編集します。

```typescript
@Get()
async findAll(): Promise<User[]> {
  return await this.usersService.findAll();
}

@Get(':id')
async findOne(@Param('id') id: number): Promise<User> {
  return this.usersService.findOne(+id);
}
```

---
layout: center
---

## サービスにfindAllとfindOneメソッドを追加

ユーザー情報を取得するメソッドを追加するため、`src/users/users.service.ts`を編集します。

```typescript
async findAll(): Promise<User[]> {
  return await this.userRepository.find().catch((e) => {
    throw new InternalServerErrorException(
      `[${e.message}]：ユーザーの取得に失敗しました。`,
    );
  });
}

async findOne(id: number): Promise<User> {
  return await this.userRepository
    .findOne({
      where: { id: id },
    })
    .then((res) => {
      if (!res) {
        throw new NotFoundException();
      }
      return res;
    })
}
```

---
layout: center
---

## ユーザー情報を取得するAPIを実行

いま作成したAPIを実行してみましょう。

```sh
# 全てのユーザーを取得するAPI
$ curl -X GET http://localhost:3000/users
[{"name":"hoge","id":1}] # 先ほど作成したユーザーが取得できている

# 特定のユーザーを取得するAPI
$ curl -X GET http://localhost:3000/users/1
{"name":"hoge","id":1}

# 存在しないユーザーを取得しようとするとエラーになる
$ curl -X GET http://localhost:3000/users/2
{"statusCode":404,"message":"Not Found"}
```

---
layout: center
---


# まとめ

以上で、NestJSの基本的な使い方を紹介しました。NestJSは、Expressをベースにしているので、Expressの知識があれば、すぐに使いこなせると思います。今回触れなかった部分も多々ありますが、今後の参考にしていただければと思います。

興味を持った方は、ぜひ、NestJSを使ってみてください。一緒にNestJSを盛り上げていきましょう！ ご興味を持っていただけた方は、ぜひ、[NestJS Japan Users Group](https://nest-jp.connpass.com/)へのご参加をお待ちしております。

[過去のイベントアーカイブ](https://www.youtube.com/@nestjsjapanusersgroup7047/streams)にも、NestJSに関する動画が載っていますので、ぜひご覧ください。

---
layout: end
---


