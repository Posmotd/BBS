<?php
$filename = 'posts.csv';

// フォームが送信された場合の処理
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $name = isset($_POST['name']) ? trim($_POST['name']) : '';
    $comment = isset($_POST['comment']) ? trim($_POST['comment']) : '';

    // 名前とコメントが空でない場合のみ処理する
    if ($name !== '' && $comment !== '') {
        $fp = fopen($filename, 'a+');

        // CSVファイルの行数を数えて投稿番号を決定
        $lines = file($filename, FILE_IGNORE_NEW_LINES);
        $postNumber = count($lines) + 1;

        // 現在の日時を取得
        $date = date('Y/m/d H:i:s');

        // CSVファイルに書き込み
        fputcsv($fp, [$postNumber, $name, $comment, $date]);
        fclose($fp);
    }
}
?>

<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>掲示板</title>
</head>
<body>
    <h1>掲示板</h1>
    <form action="" method="post">
        <label>名前: <input type="text" name="name"></label><br>
        <label>コメント: <input type="text" name="comment"></label><br>
        <button type="submit">送信</button>
    </form>

    <h2>投稿一覧</h2>
    <table border="1">
        <tr>
            <th>投稿番号</th>
            <th>名前</th>
            <th>コメント</th>
            <th>投稿日時</th>
        </tr>

        <?php
        // CSVファイルを読み込み、テーブルに表示
        if (file_exists($filename)) {
            $fp = fopen($filename, 'r');
            while ($data = fgetcsv($fp)) {
                echo '<tr>';
                echo '<td>' . htmlspecialchars($data[0]) . '</td>';
                echo '<td>' . htmlspecialchars($data[1]) . '</td>';
                echo '<td>' . htmlspecialchars($data[2]) . '</td>';
                echo '<td>' . htmlspecialchars($data[3]) . '</td>';
                echo '</tr>';
            }
            fclose($fp);
        }
        ?>
    </table>
</body>
</html>
