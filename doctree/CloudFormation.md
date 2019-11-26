# CloudFormation

### ElasticBeanstalk
定番インフラ構成の自動構築およびAppデプロイの自動化サービス
- Webサーバー構成(ELB + Auto Scaling + EC2)
- Batchワーカー構成(SQS + Auto Scaling + EC2)

### OpsWorks利用した構成管理
- Chefを

### CloudFormation
- AWSのリソース管理・構築を自動化するサービス
    - テンプレートをJSONやYAML形式で記述
	- テンプレートをもとにAWSリソースの自動構築


## CloudFormationの基本
- テンプレート
    - AWSリソースの構成をYAML or JSONで記載したドキュメント
- スタック
    - テンプレードから自動構築されたAWSリソースの集合

スタックを消すと紐ついているものを一括で消せるので便利


### テンプレート
- セクション
    - Parameters
        - 実行時に埋め込む変数値
	- Mappings
	    - 実行環境によって変わる値をMap形式で定義
	- Resources
	    - AWSリソース群を定義する
- 組み込み関数
    - Ref
	- FindInMap
- 擬似パラメータ
    - AWS::Region


sandboxで別リージョンに作るか
CloudFormationでVPCを作る
CloudFormationでsubnetを作る
CloudFormationでインターネットGWを作る
CloudFormationでEC2を作る





yarn --version


-----------------------------------------------------------------


コードの原則
The Principles of Programing

YAGNI
You Aren't Going to Need It.

PIE
Progtam Intently and Expressively.


Infrastructure as Code (IaC)








