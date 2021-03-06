https://docs.aws.amazon.com/ja_jp/emr/latest/ManagementGuide/emr-overview-arch.html

### アーキテクチャの概要

- ストレージ
- クラスターリソース管理
- データ処理フレームワーク
- アプリケーションとプログラム

### ストレージ
さまざまなファイルシステム
- Hadoop Distributed File System（HDFS）
```
分散型のスケーラブルなファイルシステムです。HDFS はデータをクラスター内の各インスタンスに分散して保存します。
データの複数のコピーが複数のインスタンスに保存されるため、個々のインスタンスが障害を起こしてもデータが失われることはありません。
HDFS はエフェメラルストレージであり、クラスターを終了するときに消去されます。
HDFS は MapReduce 処理中に中間結果をキャッシュしたり、大きなランダム I/O の発生するワークロードがある場合に便利です。
```

- EMR ファイルシステム (EMRFS) 
```
Amazon EMR で Hadoop が拡張され、まるで HDFS などのファイルシステムのように、Amazon S3 に保存されたデータに直接アクセスできます。
クラスターではファイルシステムとして HDFS または Amazon S3 のいずれかを使用できます。
ほとんどの場合、Amazon S3 は入力データおよび出力データを格納する場合に使用され、中間結果は HDFS に格納されます。
```

- ローカルファイルシステム
```
ローカルファイルシステムとは、ローカルに接続されているディスクを指します。
Hadoop クラスターを作成すると、インスタンスストアと呼ばれる、あらかじめアタッチされたディスクストレージのブロックが事前設定されている 
Amazon EC2 インスタンスから、各ノードが作成されます。
インスタンスストアボリューム上のデータは、Amazon EC2 インスタンスのライフサイクル中のみ使用できます。
```


### クラスターリソース管理

リソース管理レイヤーは、クラスターリソースの管理とデータを処理するジョブのスケジューリングを行います。

デフォルトでは、Amazon EMR は Apache Hadoop 2.0 に導入されたコンポーネントである YARN (Yet Another Resource Negotiator) を使用し、
複数のデータ処理フレームワークのクラスターリソースを集中管理します。
ただし、YARN をリソースマネージャーとして使用しない他のフレームワークやアプリケーションも Amazon EMR にあります。
Amazon EMR の各ノードには、YARN コンポーネントの管理、クラスターの正常な状態の維持、Amazon EMR サービスとのやり取りを行うエージェントもあります。

Amazon EMR には YARN ジョブをスケジュールするためのデフォルト機能があります。
Amazon EMR では、これを行うためにアプリケーションマスタープロセスの実行先としてコアノードのみを許可します。
アプリケーションマスタープロセスは、ジョブの実行を制御するため、ジョブの有効期限まで有効に存続する必要があります。

ジョブ実行制御のために組み込みの YARN ノードラベル機能を使用します

YARN ノードラベル機能のプロパティ
- yarn-site 設定分類
- capacity-scheduler 設定分類

Amazon EMR は、コアノードに CORE ラベルを自動的に付け、CORE ラベルの付いたノードでのみ
アプリケーションマスターをスケジュールするようにプロパティを設定します。


### データ処理フレームワーク

Amazon EMR で使用できる主な処理フレームワークは、Hadoop MapReduce と Spark です。

- Hadoop MapReduce
分散コンピューティングのためのオープンソースプログラミングモデルです。
これは、Map と Reduce という 2 つの機能を提供しながら、全てのロジックを処理することで並行分散アプリケーションを書くプロセスを単純化するものです。
Map 機能は「中間結果」と呼ばれるキーと値のペアにデータをマップします。
Reduce 機能は中間結果を集計し、追加アルゴリズムを適用して、最終出力を発生させます。

- Apache Spark
Spark は、ビッグデータワークロードの処理に役立つクラスターフレームワークおよびプログラミングモデルです。
Hadoop MapReduce と同様、Spark はオープンソースの分散処理システムですが、実行プランには Directed Acyclic Graphs を使用し、
データセットにはメモリ内キャッシュを利用します。
Spark を Amazon EMR で実行すると、EMRFS を使用して Amazon S3 内のデータに直接アクセスできます。
Spark では、SparkSQL などの複数のインタラクティブクエリモジュールがサポートされます。







