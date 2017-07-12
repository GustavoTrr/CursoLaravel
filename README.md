# CursoLaravel
Curso de Laravel da série "Laravel do começo ao fim" - Leandro Henrique Reis (Youtube)

https://www.youtube.com/watch?v=QtkBgWMz7O8&list=PLm7OJfCMTh6A40QXIgoa916S0uXd_JIRR

Todas as vídeo-aulas serão seguidas à risca e cada aula será etiquetada (tagueada).

Este documento será utilizado para anotar o que mais me chamou a atenção em cada aula!

Aula 1:
Instalação do Composer;
Instalação do Prestissimo (Plugin de Instalação paralela do composer);
Instalação do Laravel através do composer;

A instalação do Laravel pode ser de 2 maneiras:
1 - Baixando o instalador do Laravel pelo composer
2 - Criando diretamente um projeto pelo composer

*Lembrar para todos os comandos de sempre estar dentro da pasta correta!
composer create-project --prefer-dist laravel/laravel estoque
Após instalado o composer, iniciamos para teste:
php artisan serve

Links:
Laravel: http://www.laravel.com
Composer: https://getcomposer.org
Prestissimo: https://github.com/hirak/prestissimo
Packagist: https://packagist.org

Aula 2:
Migrations (É um método de se manter estruturas de BDs organizada e versionada)
https://tasafo.org/2012/10/13/controle-de-versao-em-bd/

Uma forma de criar uma migration é utilizando o comando do artisan:
php artisan make:migration "nome da migration"

Outra forma é se criando uma model "-m", e ele automaticamente já criará a migration e a a classe model
php artisan make:model "nome da model"

ao criar um model, é importante:
 - nome de model começa com maiúsculo!
  - No singular!
  - nome da tabela é no plural!
  *Isso é padrão do Laravel
  
É interessante utilizar palavras em inglês pois o Laravel pode fazer alguma interpretação delas no sentido de facilitar a programação.

A função timestamps() é utilizada para gerar as colunas de auditoria (created_at e updated_at)
softDeletes() é um método que cria uma coluna na tabela do BD, para que seja registrado quando aquele registro for deletado, sem de fato excluir os dados

Configurar dados de conexão de BD no arquivo no arquivo ".env"

Realizamos a construção do banco de dados diretamente pelo SGBD, e depois seguimos com o código pelo CMD (Terminal):
php artisan migrate

Surge um problema:
[Illuminate\Database\QueryException] SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table users add unique users_email_unique(email))
Então, após pesquisa na Internet, descubro que este problema já é identificado pela documentação do Laravel e é solucionado da seguinte maneira:
Acessa o arquivo app/Providers/AppServiceProvider.php
No início dele se insere o código: use Illuminate\Support\Facades\Schema;
E no método boot(), se insere o código: Schema::defaultStringLength(191);

Fontes:
https://github.com/laravel/framework/issues/17508
https://laravel.com/docs/5.4/migrations#indexes

Adicionei ao projeto o gitignore e dentro dele inseri ".env" para que ele ignore os arquivos com extensão .env
pois cada arquivo deste deve ser setado com as configurações do ambiente (enviroment) em que se encontra.


Aula 3:
Usando git e GitHub

Criamos o gitignore com a seguinte configuração:
/vendor
/node_modules
/public/storage
Homestead.yaml
Homestead.json
.env

Na verdade o Laravel já traz em si arquivos .gitignore em cada pasta conforme necessário.

Aula 4:
Factories e Fakers

Factories é um mecanismo disponível no Laravel que facilita testes e ajuda a popular tabelas de banco de dados

https://laravel-news.com/learn-to-use-model-factories-in-laravel-5-1

"When creating seed data in the past you could utilize Eloquent or Laravel’s query builder and that way is still supported. However, with the introduction of model factories you can use them to build out “dummy” models which can be used for both seed data and in testing."

Please Note: If your app is going to send real email then you should utilize $faker->safeEmail instead of just ->email. The reason for this is ->email can potentially generate a real email, where safeEmail uses example.org that is reserved by RFC2606 for testing purposes.

Usamo o Tinker, um recurso do láravel para dar comandos ao php pelo cmd. É um mecanismo Read–Eval–Print Loop (REPL)

Uma prática interessante é na função up da migration de usuários um usuário admin padrão para o desenvolvimento
!Essa prática exige cuidado!!

Links: 
Biblioteca faker: https://github.com/fzaninotto/Faker