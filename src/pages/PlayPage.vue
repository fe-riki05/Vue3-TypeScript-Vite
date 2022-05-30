<script lang="ts" setup>
// 3-1 で作成したテトリスのフィールドを定義するコード
const row = 20;
const column = 10;

const field = new Array(row);

for (let i = 0; i < row; i++) {
  const fieldColumn = new Array(column).fill(0);
  field[i] = fieldColumn;
}

// 画面最上部の左端に縦の I-テトリミノを配置する
field[0][0] = 1;
field[1][0] = 1;
field[2][0] = 1;
field[3][0] = 1;

// 各テトリミノに対応した CSS のクラス名を取得する関数
const classBlockColor = (x: number, y: number): string => {
  // 1. テトリスのフィールドのマス目の状態を取得する
  const type = field[y][x];

  // 2. マス目の状態に応じて描画に適切な CSS クラス名を取得する
  if (type > 0) {
    switch (type) {
      case 1:
        // 1: I-テトリミノ（水色）
        return "block-i";
      case 2:
        // 2: O-テトリミノ（黄色）
        return "block-o";
      case 3:
        // 3: S-テトリミノ（緑）
        return "block-s";
      case 4:
        // 4: Z-テトリミノ（赤）
        return "block-z";
      case 5:
        // 5: J-テトリミノ（青）
        return "block-j";
      case 6:
        // 6: L-テトリミノ（オレンジ）
        return "block-l";
      case 7:
        // 7: T-テトリミノ（紫）
        return "block-t";
      default:
        // 0 (1~7以外): 空白
        return "";
    }
  }
};
</script>

<template>
  <h1>プレイ画面</h1>
  <h2>ユーザー名: {{ $route.query.name }}</h2>

  <div class="container">
    <table class="field" style="border-collapse: collapse">
      <tr
        v-for="(row, y) in field"
        :key="y">
        <!-- テトリスのフィールドの各マス目にその状態を描画する (0: 空白, 1: I-テトリミノ, etc.) -->
        <td
          class="block"
          v-for="(col, x) in row"
          :key="() => `${x}${y}`"
          :class="classBlockColor(x, y)"
        />
      </tr>
    </table>
  </div>
</template>

<!-- スタイルシートに SCSS 記法 (Sass) を利用する -->
<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: stretch;
}

.field {
  border: ridge 0.4em #2c3e50;
  border-top: none;
}

.block {
  width: 1em;
  height: 1em;
  border: 0.1px solid #95a5a6;

  /*
  各テトリミノに対応した色を扱うクラス定義
  .block-i, .block-o のようにクラスが定義される
  */
  &-i {
    background: #3498db;
  }
  &-o {
    background: #f1c40f;
  }
  &-t {
    background: #9b59b6;
  }
  &-j {
    background: #1e3799;
  }
  &-l {
    background: #e67e22;
  }
  &-s {
    background: #2ecc71;
  }
  &-z {
    background: #e74c3c;
  }
}
</style>
