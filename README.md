# ニューラルネットワーク計算

## sigmoid函数

$$
    a_i*x_i+b_i=k_i
$$
$$
    l_i = \sigma(k_i) = \frac{1}{1 + e^{-k_i}}
$$
$$
    O = \sum_{i=1}^{n} l_i
$$
$$
    y = \sigma(O) = \frac{1}{1 + e^{-O}}
$$
とする。
$$
    E = (y - t)^2
$$
$$ \frac{dE}{da_i} $$
は連鎖律より以下ののようになる。
$$
    \frac{dE}{da_i} = \frac{dE}{dy} \cdot \frac{dy}{dO} \cdot \frac{dO}{dl_i} \cdot \frac{dl_i}{dk_i} \cdot \frac{dk_i}{da_i}
$$

それぞれの項を計算すると以下のようになる。

$$
    \frac{dE}{dy} = \frac{d(y-t)^2}{dy} =  \frac{d(y^2+t^2-2yt)}{dy} = 2y-2t = 2(y - t)
$$
$$
    \frac{dy}{dO} = y(1-y)
$$
$$
    \frac{dO}{dl_i} = 1
$$
$$
    \frac{dl_i}{dk_i} = l_i(1-l_i)
$$
$$
    \frac{dk_i}{da_i} = x_i
$$
$$
    \frac{dk_i}{db_i} = 1
$$

より

$$
    \frac{dE}{da_i} = 2(y - t) \cdot y(1-y) \cdot l_i(1-l_i) \cdot x_i
$$
$$
    \frac{dE}{db_i} = 2(y - t) \cdot y(1-y) \cdot l_i(1-l_i)
$$

### 重みの更新

$$
    a_i \leftarrow a_i - \eta \cdot \frac{dE}{da_i}
$$
$$
    b_i \leftarrow b_i - \eta \cdot \frac{dE}{db_i}
$$

## ReLU函数
先程のsigmoid函数をReLU函数に置き換えると以下のようになる。

$$
    a_i*x_i+b_i=k_i
$$
$$
    l_i = ReLU(k_i) = \max(0, k_i)
$$
$$
    O = \sum_{i=1}^{n} l_i
$$
$$
    y =ReLU(O) = \max(0, O);
$$

とする。

$$
    E = (y - t)^2
$$
$$ 
  \frac{dE}{da_i}
$$

は連鎖律より以下ののようになる。

$$
    \frac{dE}{da_i} = \frac{dE}{dy} \cdot \frac{dy}{dO} \cdot \frac{dO}{dl_i} \cdot \frac{dl_i}{dk_i} \cdot \frac{dk_i}{da_i}
$$

それぞれの項を計算すると以下のようになる。

$$
    \frac{dE}{dy} = \frac{d(y-t)^2}{dy} =  \frac{d(y^2+t^2-2yt)}{dy} = 2y-2t = 2(y - t)
$$
$$
    \frac{dy}{dO} = \max(0, O) > 0 ? 1 : 0
$$
$$
    \frac{dO}{dl_i} = 1
$$
$$
    \frac{dl_i}{dk_i} = \max(0, k_i) > 0 ? 1 : 0
$$
$$
    \frac{dk_i}{da_i} = x_i
$$
$$
    \frac{dk_i}{db_i} = 1
$$

より

$$
    \frac{dE}{da_i} = 2(y - t) \cdot (\max(0, O) > 0 ? 1 : 0) \cdot (\max(0, k_i) > 0 ? 1 : 0) \cdot x_i
$$
$$
    \frac{dE}{db_i} = 2(y - t) \cdot (\max(0, O) > 0 ? 1 : 0) \cdot (\max(0, k_i) > 0 ? 1 : 0)
$$

### 重みの更新

$$
    a_i \leftarrow a_i - \eta \cdot \frac{dE}{da_i}
$$
$$
    b_i \leftarrow b_i - \eta \cdot \frac{dE}{db_i}
$$
