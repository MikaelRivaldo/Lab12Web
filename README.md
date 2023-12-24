# Lab12Web

# DDL: Table User

```html
CREATE TABLE `user`(
`id` INT NOT NULL AUTO_INCREMENT,
`username` VARCHAR(50),
`password` VARCHAR(50),
PRIMARY KEY (`id`),
UNIQUE INDEX `UNIQUE` (`username`)
) ENGINE=MYISAM;

INSERT INTO `user` (`username`, `password`) VALUES ('admin'
, md5('admin'));
```
![image](https://github.com/MikaelRivaldo/Lab12Web/assets/115770247/c23a7b74-dc9e-459f-a966-70a11d519abe)

# Selanjutnya membuat `Login_season.php`

```html
<?php

session_start();
if (!isset($_SESSION['isLogin']))
    header('location: login.php');

```

# Selanjutnya membuat `Login.php`

```html
<?php
session_start();

$title = 'Data Barang';
include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $user = $_POST['user'];
    $password = $_POST['password'];

    $sql = "SELECT * FROM user WHERE username = '{$user}'
AND password = md5('{$password}') ";
    $result = mysqli_query($conn, $sql);
    if ($result && mysqli_affected_rows($conn) != 0) {
        $_SESSION['isLogin'] = true;
        $_SESSION['user'] = mysqli_fetch_array($result);

        header('location: index.php');
    } else
        $errorMsg = "<p style=\"color:red;\">Gagal Login,
silakan ulangi lagi.</p>";
}

include_once "header.php";

if (isset($errorMsg)) echo $errorMsg;
?>

<h2>Login</h2>
<form method="post">
    <div class="input">
        <label>Username</label>
        <input type="text" name="user" />
    </div>
    <div class="input">
        <label>Password</label>
        <input type="password" name="password" />
    </div>
    <div class="submit">
        <input type="submit" name="submit" value="Login" />
</form>
<?php
include_once 'footer.php';
?>
```

