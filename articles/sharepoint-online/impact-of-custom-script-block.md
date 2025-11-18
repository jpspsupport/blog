---
title: (MC714186) カスタム スクリプトのブロックによる影響について
date: 2024-09-02
tags:
  - SharePoint Online
---

この投稿では、Microsoft 365 管理センターのメッセージ センターに MC714186 として掲載されている、SharePoint Online のカスタム スクリプトの無効化について記載します。
多くの場合はカスタム スクリプトのブロックによる既存スクリプトへの影響はありませんが、特定の SharePoint Framework ソリューション（requiresCustomScript プロパティが True に設定されたソリューション）をご利用の場合は、影響を受ける可能性がありますのでご確認ください。  
※カスタム スクリプトのブロックに関する最新の情報は、メッセージ センターにて MC714186 をご確認ください。

<!-- more -->

## カスタム スクリプトのブロックの概要

SharePoint サイトでは、管理者がカスタム スクリプトの実行を許可することで、ページへのスクリプトの追加や、スクリプトが含まれるファイルのアップロード、ソリューションの追加など、柔軟にサイトをカスタマイズできるようになります。(※1)
しかしながら、サイトの編集権限を持つ一般ユーザーが容易にスクリプトを常時追加できるようになるため、悪意のあるスクリプトが挿入されるなどのセキュリティへの注意が必要です。(※2)  
このようなセキュリティ リスクを軽減するため、今後(※3)は一部のテンプレートを除くすべてのサイト(※4)で、カスタム スクリプトの編集が自動的にブロックされるように変更されます。
サイトへのスクリプトの追加、変更、または削除が必要となった場合は、テナント管理者がサイトのカスタム スクリプトを一時的に許可（有効化）することで、以前と同様にスクリプトを追加することができます。
カスタム スクリプトの有効化後は、24 時間以内に再び自動で無効化されます。セキュリティ強化を目的として、スクリプトの追加完了後に管理者が手動で無効化に戻すことも可能です。

(※1) [カスタム スクリプトを許可または禁止する - SharePoint in Microsoft 365 | Microsoft Learn](https://learn.microsoft.com/ja-jp/sharepoint/allow-or-prevent-custom-script#features-affected-when-custom-script-is-blocked)  

(※2) [カスタム スクリプトを許可する場合のセキュリティに関する考慮事項 - SharePoint in Microsoft 365 | Microsoft Learn](https://learn.microsoft.com/ja-jp/sharepoint/security-considerations-of-allowing-custom-script)

(※3) カスタム スクリプトの無効化は、2024 年 4 月下旬に開始され、5 月上旬までに完了する予定です。最新の展開状況は[メッセージ センターの MC714186](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC714186) をご確認ください。

(※4) カスタム スクリプトの無効化は、以下のサイト テンプレートを除くすべての既存の SharePoint サイトと OneDrive サイトに適用されます。

BLANKINTERNETCONTAINER#0 = 従来の発行ポータル サイト  
CMSPUBLISHING#0 = 公開サイト  
BLANKINTERNET#0 = 発行サイト    
~~GROUP#0 = チーム サイト~~
~~APPCATALOG#0 = アプリ カタログ~~
CSPCONTAINER#0 = CSP コンテナー  

※ 2024 年 8 月 28 日 更新
カスタム スクリプトの無効化の対象外のサイト テンプレートから「GROUP#0 = チーム サイト」が除外されました。
「GROUP#0 = チーム サイト」は MC714186 の変更によりカスタム スクリプトが無効化されます。

※ 2025 年 11 月 18 日 更新
カスタム スクリプトの無効化の対象外のサイト テンプレートから「APPCATALOG#0 = アプリ カタログ」が除外されます。
「APPCATALOG#0 = アプリ カタログ」は MC1186368 の変更により、2026 年 1 月中旬以降、カスタム スクリプトが無効化されます。
最新のスケジュールは MC1186368 をご確認ください。

## 注意事項 (例外)
カスタム スクリプトのブロック後も、OneDrive サイトと SharePoint サイトの既存ページのスクリプトの実行は一般的に影響を受けません。  
しかしながら、SharePoint Framework ソリューションにおいて、マニフェストで requiresCustomScript プロパティを True に設定している場合、カスタム スクリプトのブロックによりソリューションが動作しなくなることを確認しております。requiresCustomScript プロパティが True に設定されているソリューションの一例として、PnP の Modern Script Editor Web Part (https://github.com/pnp/sp-dev-fx-webparts/blob/main/samples/react-script-editor/README.md) があります。
~~requiresCustomScript プロパティが True に設定された SharePoint Framework ソリューションをご利用の場合は、ブロックの期限が迫っておりますので、カスタム スクリプトの無効化適用をあらかじめ延長することをご検討くださいますようお願いいたします。~~

※ 2024 年 11 月 19 日 更新
カスタム スクリプトの無効化の延長は 2024 年 11 月中旬までとなります。requiresCustomScript プロパティが True に設定された SharePoint Framework ソリューションをご利用の場合は、requiresCustomScript プロパティを Flase に変更してソリューションを再追加するか、ソリューション利用時のみ一時的にカスタム スクリプトを有効化することをご検討くださいますようお願いいたします。

~~なお、この問題については、2024 年 4 月 10 日現在、開発部門にて調査が進められております。調査の進展があり次第、本記事を更新いたします。~~

※ 2024 年 9 月 2 日 更新
上記は製品の想定動作であり、今後、カスタム スクリプトがブロックされているサイトでは、requiresCustomScript プロパティが True に設定されている SharePoint Framework ソリューションは動作しませんので、ご留意ください。
この内容は以下の公開情報にも掲載されています。
[カスタム スクリプトを許可または禁止する - SharePoint in Microsoft 365 | Microsoft Learn](https://learn.microsoft.com/ja-jp/sharepoint/allow-or-prevent-custom-script#features-affected-when-custom-script-is-blocked)

(*) requiresCustomScript プロパティの設定例が掲載された公開情報
https://learn.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/build-a-hello-world-web-part#web-part-manifest

## カスタム スクリプトの無効化の延長について
~~カスタム スクリプトの無効化を遅らせるための SharePoint 管理シェル コマンド DelayDenyAddAndCustomizePagesEnforcement が 4 月中旬までに展開されます。~~
~~SharePoint 管理者もしくは全体管理者で以下のコマンドを実行することで、カスタム スクリプトの無効化を 2024 年 11 月中旬まで遅らせることが可能です。~~
<!-- ``` PowerShell -->
~~Set-SPOTenant -DelayDenyAddAndCustomizePagesEnforcement $True~~
<!-- ``` -->

※ 2024 年 11 月 19 日 更新
カスタム スクリプトの無効化を遅らせるための SharePoint 管理シェル コマンド DelayDenyAddAndCustomizePagesEnforcement による延長は 2024 年 11 月中旬までとなります。以降は、カスタム スクリプトの有効化後、24 時間経過後に再び自動で無効化されます。

今回の投稿は以上です。
不明な点などがありましたら、弊社サポートサービスまでお気軽にお問い合わせください。
