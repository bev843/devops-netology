# devops-netologyfirsl line
first line

qw

qwe

___
Исключаются все файлы директории .terraform, находящейся в любом месте начиная от директории, в которой расположен файл .gitignore

`**/.terraform/*`

Исключаются все файлы с данными именами, находящиеся в любом месте дерева каталогов, от директории, где расположен .gitignore :
`crash.log`
`override.tf`
`override.tf.json`
`.terraformrc`
`terraform.rc`

Исключаются все файлы с масками имен (где * - любое количество символов, в том числе и 0), находящиеся в любом месте дерева каталогов, от директории, где расположен .gitignore :
`*.tfstate` 
`*.tfstate.*`
`*.tfvars`
`*_override.tf`
`*_override.tf.json`

another new line from PyCharm
