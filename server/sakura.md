# さくらサーバを今後どうしていくか

さくらVPS
３つ

## サーバA

コスト: 15,000/年

image
http://ssssssssss.jpg
http://ssssssssss.json

> S3にする
> S3 標準 - 低頻度アクセス
> 標準 <-> 低頻度の切り替えも簡単

## サーバB

コスト: 800/月

railsで作ったAPI
railsで作った管理画面
Let's Encrypt
https://ssssss.ssssss

> API Gateway + Lambda 
> parameter store なら無料
> 複雑ならDynamo
> S3にjsonをおいて、lambdaがそれを見にいく感じ
> バケットを分ける

## サーバC

コスト: 500/月

PDFのファイルサーバ
http://aaaaaaaaaaaaa.pdf

> S3にする
> S3 標準 - 低頻度アクセス

AWSでドメイン使うと $0.5/mon
S3のURLを、今と同じURLにすることも可能
URLが複雑で再現むずいなら、Cloud Front を使うこともできる
SSLするならCloud Front 必須、証明書はAWSがくれるはず
サービス断が一瞬発生（起きないかも）

お名前.comのドメイン設定を



 native患者が存在している && 閲覧許可をしている場合 && アプリ導線がTrueになっている場合
            patient_app_patient
            and patient_app_patient.visible_pharmacy_admin
            and request.user.pharmacy.visible_linkage_native_app


