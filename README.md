<?php
session_start();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Dil değiştirme işlemi
    if (isset($_POST["language"])) {
        $selectedLanguage = $_POST["language"];
        $_SESSION["language"] = $selectedLanguage;
    } else {
        $username = $_POST['username'];
        $password = $_POST['password'];

        if ($username == 'admin' && $password == '1234') {
            // Kullanıcı girişi başarılı
            $_SESSION['username'] = $username;

            // Dashboard sayfasına yönlendirme
            header("Location: dashboard.php");
            exit();
        } else {
            $loginError = "Kullanıcı adı veya şifre yanlış.";
        }
    }
}

// Oturumdaki dil tercihini alın
$language = isset($_SESSION["language"]) ? $_SESSION["language"] : "tr"; // Varsayılan dil: Türkçe
?>

<!DOCTYPE html>
<html>
<head>
    <title><?php echo ($language === 'en') ? 'Login' : 'Giriş Yap'; ?></title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #36393f;
            margin: 0;
            padding: 0;
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            max-width: 500px;
            width: 100%;
            padding: 20px;
            background-color: #2c2f33;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .container h2 {
            margin-bottom: 20px;
            color: #fff;
            text-align: center;
        }

        .form-input {
            width: 96%;
            padding: 10px;
            margin-bottom: 15px;
            border: none;
            background-color: #40444b;
            color: #fff;
        }

        .form-button {
            background-color: #7289da;
            color: #fff;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            width: 100%;
        }

        .error-message {
            color: red;
            text-align: center;
        }

        /* Dil Değiştirme Formu Stilleri */
        .language-form {
            background-color: #2c2f33; /* Ayarlar sayfasındaki arka plan rengi */
            padding: 20px;
            border-radius: 5px;
            margin-top: 20px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .language-form h2 {
            color: #fff;
            margin-bottom: 10px;
            text-align: center;
        }

        .language-form label {
            display: block;
            margin-bottom: 5px;
            color: #fff;
        }

        .language-form select {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: none;
            border-radius: 3px;
            background-color: #36393f;
            color: #fff;
            font-size: 16px;
        }

        .language-form button {
            background-color: #7289da;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 3px;
            cursor: pointer;
            width: 100%;
        }

        .language-form button:hover {
            background-color: #5469d4;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2><?php echo ($language === 'en') ? 'Login' : 'Giriş Yap'; ?></h2>
        <?php if (isset($loginError)) : ?>
            <p class="error-message"><?php echo $loginError; ?></p>
        <?php endif; ?>
        <form method="POST" action="">
            <input class="form-input" type="text" name="username" placeholder="<?php echo ($language === 'en') ? 'Username' : 'Kullanıcı Adı'; ?>" required>
            <input class="form-input" type="password" name="password" placeholder="<?php echo ($language === 'en') ? 'Password' : 'Şifre'; ?>" required>
            <input class="form-button" type="submit" value="<?php echo ($language === 'en') ? 'Login' : 'Giriş Yap'; ?>">
        </form>

        <!-- Dil Değiştirme Formu -->
        <div class="language-form">
            <h2><?php echo ($language === 'en') ? 'Change Language' : 'Dil Değiştir'; ?></h2>
            <form method="post">
                <label for="language"><?php echo ($language === 'en') ? 'Language:' : 'Dil:'; ?></label>
                <select id="language" name="language">
                    <option value="tr" <?php echo ($language === 'tr') ? 'selected' : ''; ?>>Türkçe</option>
                    <option value="en" <?php echo ($language === 'en') ? 'selected' : ''; ?>>İngilizce</option>
                </select>
                <button type="submit"><?php echo ($language === 'en') ? 'Change Language' : 'Dili Değiştir'; ?></button>
            </form>
        </div>
        <!-- Dil Değiştirme Formu Sonu -->
    </div>
</body>
</html>
