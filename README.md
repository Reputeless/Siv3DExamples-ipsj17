『情報処理』2017 年 6 月号 掲載  
**音や画像で遊ぼう ～インタラクティブアプリケーションのための C++ フレームワーク「Siv3D」～**  
サンプルコード

## 1. コンピュータ画伯
```cpp
# include <Siv3D.hpp>

// ① 2つの画像の差分を計算
double Diff(const Image& a, const Image& b) {
	double d = 0.0;
	for (auto p : step(a.size))
	{
		d += Abs(int(a[p].r) - int(b[p].r));
		d += Abs(int(a[p].g) - int(b[p].g));
		d += Abs(int(a[p].b) - int(b[p].b));
	}
	return d;
}

void Main() {
	// ② 目標とする画像を開く
	const Image target = Dialog::OpenImage()
		.fit(Window::Size());
	// ③ 同じ大きさの白い画像を用意
	Image image(target.size, Palette::White);
	Image old = image;
	DynamicTexture texture(old);
	double d1 = Diff(target, image); // ④

	while (System::Update()) {
		for (int i = 0; i < 100; ++i) {
			old = image; // ⑤

			// ⑥ 画像内のランダムな位置
			Point pos = RandomPoint(
				image.width, image.height);
			// ⑦ ランダムな色
			ColorF color;
			color.r = Random();
			color.g = Random();
			color.b = Random();
			color.a = Random();
			// ⑧ ランダムな大きさ
			int size = Random(1, 10);
			// ⑨ 円を描いてみる
			Circle(pos, size).write(image, color);

			// ⑩ 目標に近づけば採用
			double d2 = Diff(target, image);
			if (d2 < d1) {
				d1 = d2;
			}
			else {
				image = old; // ⑪
			}
		}

		// ⑫ テクスチャを更新して描画
		texture.fill(image);
		texture.draw();
	}
}
```


## 2. あなたの声はどんな形

```cpp


```

## 3. 幸せになれる画像ビューア

```cpp


```

## 4. めちゃくちゃな音楽プレイヤ

```cpp


```

## 5. 数式の大地を探検する

```cpp


```
