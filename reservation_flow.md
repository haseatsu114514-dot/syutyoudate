# 予約システムの流れとコスト

## フロー図

```mermaid
flowchart TD
    %% ノード定義（さらに細かく改行）
    Step1("<b>LINE予約開始</b><br/>コースを選択後、<br/>カレンダーを参照して<br/><u>空いている日時のみ</u><br/>表示・選択")
    Step2("<b>フォーム入力</b><br/>名前・電話番号<br/>住所などを記入")
    
    Notify("<b>受付通知</b><br/>承認待ちの連絡")
    Check{"管理者<br/>確認"}
    
    Approve["承認"]
    Reject["お断り"]
    
    Confirm("<b>確定通知</b><br/>予約内容の<br/>リマインド")
    Decline("<b>お断り通知</b><br/>キャンセルの<br/>連絡")

    %% フロー接続
    Step1 --> Step2
    Step2 --> Notify
    Notify --> Check
    
    Check -- OK --> Approve
    Check -- NG --> Reject
    
    Approve --> Confirm
    Reject --> Decline

    %% スタイル定義
    classDef free fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#0D47A1;
    classDef paid fill:#FFEBEE,stroke:#C62828,stroke-width:2px,color:#B71C1C;
    
    class Step1,Step2 free;
    class Notify,Confirm,Decline paid;
```

## ポイント
**★ カレンダー自動照合**
LINEで日時を選ぶ際、システムが自動でGoogleカレンダーの空き状況を確認するため、**「空いている時間」だけが選択肢として表示されます。** これによりダブルブッキングを防げます。

## テキスト版フロー

**【ステップ1】 ユーザーの操作 (無料)**
1. **LINE**
   コース選択後、カレンダーを参照して**空いている日時のみ**を表示・選択
   ↓
2. **フォーム**
   フォーム上で名前や電話・住所を記入

**【ステップ2】 通知と確認 (有料)**
3. **通知**
   受付完了（承認を待つよう通知）
   ↓
4. **確認**
   管理者が内容を確認

**【ステップ3】 結果の連絡 (有料)**
- **承認の場合**: 予約確定の連絡（双方に予約内容リマインド）
- **お断りの場合**: お断りの連絡
