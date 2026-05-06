# 開発環境のセットアップガイド

## 必要な環境
- Node.js 16以上
- npm または yarn

## インストール手順

### 1. 依存パッケージのインストール
```bash
npm install
```

### 2. 開発サーバーの起動
```bash
npm run dev
```
ブラウザで http://localhost:3000 にアクセスしてください。

### 3. ビルド
```bash
npm run build
```
`dist` フォルダにプロダクション用ファイルが生成されます。

## プロジェクト構成の説明

### `/src/types/index.ts`
- アプリケーション全体で使用する型定義

### `/src/utils/`
- **storage.ts**: LocalStorageを使用したデータ永続化
- **levelCalculator.ts**: レベル計算、背景・称号のアンロック判定
- **statistics.ts**: 統計情報の計算、時間フォーマット
- **backgroundManager.ts**: 背景と称号のスタイル管理

### `/src/hooks/`
- **useTimer.ts**: タイマーロジック（ブラウザクローズ対応）
- **useStudyData.ts**: データ管理
- **useLevelSystem.ts**: レベルシステム管理

### `/src/components/`
- **HomeScreen.tsx**: ホーム画面
- **StopwatchMode.tsx**: ストップウォッチ画面
- **PomodoroMode.tsx**: ポモドーロ画面
- **SubjectSelector.tsx**: 科目選択コンポーネント
- **StatisticsScreen.tsx**: 統計情報画面
- **LevelScreen.tsx**: レベル・背景・称号管理画面

## 主な実装ポイント

### ブラウザクローズ後のタイマー復旧
`useTimer.ts`の`useEffect`で、ブラウザクローズ時の経過時間を計算して復旧しています。

### データの永続化
すべてのデータはLocalStorageに保存されます。`storage.ts`から利用可能。

### レベル計算
勉強時間からレベルを算出し、背景と称号を自動でアンロック。

## トラブルシューティング

### ポート3000が既に使用されている場合
```bash
npm run dev -- --port 3001
```

### 古いデータが残っている場合
ブラウザの開発者ツール → アプリケーション → LocalStorage から削除してください。

## 機能の追加・カスタマイズ

### 背景を追加する場合
`src/utils/backgroundManager.ts`の`BackgroundStyle`に新しいグラデーションを追加してください。

### 称号を追加する場合
`getTitleName`と`getAllTitleIds`を編集してください。

### 科目を追加する場合
`src/types/index.ts`の`Subject`型と`SubjectLabels`を編集してください。

## パフォーマンス最適化
- React.memoやuseCallbackを活用
- 不要な再レンダリングを防止
- LocalStorageの定期的なクリーンアップ

---

何か質問や問題があれば、お気軽にお聞きください！
