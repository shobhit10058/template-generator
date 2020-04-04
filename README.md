# Online Judge Template Generator

[![test](https://github.com/kmyk/online-judge-template-generator/workflows/test/badge.svg)](https://github.com/kmyk/online-judge-template-generator/actions)
[![Documentation Status](https://readthedocs.org/projects/online-judge-template-generator/badge/)](https://online-judge-template-generator.readthedocs.io/en/latest/)
[![PyPI](https://img.shields.io/pypi/v/online-judge-template-generator)](https://pypi.org/project/online-judge-template-generator/)
[![LICENSE](https://img.shields.io/pypi/l/online-judge-template-generator.svg)](https://github.com/kmyk/online-judge-template-generator/blob/master/LICENSE)

(CAUTION: the current version is unstable. see [Compatibility](https://online-judge-template-generator.readthedocs.io/en/latest/compatibility.html)
/ 注意: 現在はまだ開発中のバージョンです。[互換性について](https://online-judge-template-generator.readthedocs.io/en/latest/compatibility.html)は読んでおいてください)

## What is this

競技プログラミングテンプレートを作ってくれるやつです。
[kyuridenamida/atcoder-tools](https://github.com/kyuridenamida/atcoder-tools) を参考に、その本質部分だけを抜き出して再実装しました。
内部構造については [How it works](https://online-judge-template-generator.readthedocs.io/en/latest/how-it-works.html) に書かれています。

主目的は以下のふたつです:

-   不適切な入出力方法を用いたことによる TLE を回避すること。たとえば「Codeforces で `std::endl` を使って TLE する」みたいなのをなくしたい
-   ランダムケースを生成してのテストを気軽に行えるようにすること。たとえば、サンプル AC して提出してみたら謎の WA が出たとき「これランダムケース生成して愚直解と比較すれば原因分かるだろうけど、面倒なんだよな」ってなりがちですが、この面倒を半減させ高速にデバッグできるようにしたい


## How to install

``` console
$ pip3 install online-judge-template-generator
```


## Usage

`oj-template` コマンドは、指定された問題に対し、入出力パートを自動生成します。
入出力解析は AtCoder と yukicoder と [Library Checker](https://judge.yosupo.jp/) にのみ対応していますが、それら以外でも一応は動きます。

``` console
$ oj-template [-t TEMPLATE] URL
```

`oj-contest` コマンドは、指定された問題やコンテストに対し、テンプレート生成やサンプルのダウンロードを一括で行います。
[`oj` コマンド](https://github.com/kmyk/online-judge-tools) が動くやつなら何に対してでも動きます。

``` console
$ oj-contest URL
```


### Generating random cases

ランダムケースの生成は、`oj-contest` コマンドがデフォルトで生成する `generate.py` を修正した後に、次のように実行してください。

``` console
$ oj generate-input "python3 generate.py"
```

ファイル `generate.py` は `oj-template -t generate.py "https://..."` というコマンドの実行によっても生成できます。

また、ランダムケース生成を補助するための module `onlinejudge_random` が用意されています。詳細は[ドキュメント](https://online-judge-template-generator.readthedocs.io/en/latest/onlinejudge_random.html)を確認してください。


## Examples

``` console
$ oj-template https://codeforces.com/contest/1300/problem/D
...

#include <bits/stdc++.h>
#define REP(i, n) for (int i = 0; (i) < (int)(n); ++ (i))
#define REP3(i, m, n) for (int i = (m); (i) < (int)(n); ++ (i))
#define REP_R(i, n) for (int i = (int)(n) - 1; (i) >= 0; -- (i))
#define REP3R(i, m, n) for (int i = (int)(n) - 1; (i) >= (int)(m); -- (i))
#define ALL(x) ::std::begin(x), ::std::end(x)
using namespace std;

const string YES = "YES";
const string NO = "nO";
bool solve(int vam, const vector<int64_t> & kfi, const vector<int64_t> & vkw) {
    // TODO: edit here
}

// generated by online-judge-template-generator (https://github.com/kmyk/online-judge-template-generator)
int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    constexpr char endl = '\n';
    int vam;
    cin >> vam;
    vector<int64_t> kfi(vam), vkw(vam);
    REP (i, vam) {
        cin >> kfi[i] >> vkw[i];
    }
    bool ans = solve(vam, kfi, vkw);
    cout << (ans ? YES : NO) << endl;
    return 0;
}
```

``` console
$ oj-template -t generate.py https://judge.yosupo.jp/problem/staticrmq
...

#!/usr/bin/env python3
import random
import onlinejudge_random as random_oj

def main():
    N = random.randint(1, 10 ** 9)  # TODO: edit here
    a = [None for _ in range(N)]
    Q = random.randint(1, 10 ** 9)  # TODO: edit here
    l = [None for _ in range(Q)]
    r = [None for _ in range(Q)]
    for i in range(N):
        a[i] = random.randint(1, 10 ** 9)  # TODO: edit here
    for i in range(Q):
        l[i] = random.randint(1, 10 ** 9)  # TODO: edit here
        r[i] = random.randint(1, 10 ** 9)  # TODO: edit here
    print(N, Q)
    print(*[a[i] for i in range(N)])
    for i in range(Q):
        print(l[i], r[i])

if __name__ == "__main__":
    main()
```

``` console
$ oj-contest https://atcoder.jp/contests/abc158
...

$ tree ~/atcoder.jp
/home/ubuntu/atcoder.jp
└── abc158
    ├── abc158_a
    │   ├── main.cpp
    │   ├── main.py
    │   ├── generate.py
    │   └── test
    │       ├── sample-1.in
    │       ├── sample-1.in
    │       ├── sample-1.out
    │       ├── sample-2.in
    │       ├── sample-2.out
    │       ├── sample-3.in
    │       └── sample-3.out
    ├── ...
    ├── ...
    ├── ...
    ├── ...
    └── abc158_f
        ├── main.cpp
        ├── main.py
        ├── generate.py
        └── test
            ├── sample-1.in
            ├── sample-1.out
            ├── sample-2.in
            ├── sample-2.out
            ├── sample-3.in
            ├── sample-3.out
            ├── sample-4.in
            └── sample-4.out

13 directories, 50 files
```


## Settings

`oj-template` のためのテンプレートは `~/.config/online-judge-tools/template/` の下に `~/.config/online-judge-tools/template/customized.py` のように作って `oj-template -t customized.py https://...` のように指定する。
テンプレート記法は [Mako](https://www.makotemplates.org/) のものを使う。
[fastio.cpp](https://github.com/kmyk/online-judge-template-generator/blob/master/onlinejudge_template_resources/template/fastio.cpp) とか [customize_sample.cpp](https://github.com/kmyk/online-judge-template-generator/blob/master/onlinejudge_template_resources/template/customize_sample.cpp) とかを見てそれっぽく書けば動く。

`oj-contest` の設定は `~/.config/online-judge-tools/oj2.config.toml` に次のように設定する。

``` toml
contest_directory = "~/Desktop/{service_domain}/{contest_id}/{problem_id}"
problem_directory = "."

[templates]
"main.py" = "main.py"
"naive.py" = "main.py"
"generate.py" = "generate.py"
```

設定項目:

-   `problem_directory` (string): 問題の URL が指定された場合は `{problem_directory}` にファイルが用意される。
    -   default: `.`
    -   使える変数:
        -   `{problem_id}`: 問題 ID (`abc123_d` など)
-   `contest_directory` (string): コンテストの URL が指定された場合は `{contest_directory}/{problem_directory}` にファイルが用意される。(default: 
    -   default: `{problem_id}`
    -   使える変数:
        -   `{problem_id}`: 問題 ID (`abc123_d` など)
        -   `{contest_id}`: コンテスト ID (`abc123` など)
        -   `{service_domain}`: サービスのドメイン (`atcoder.jp` など)
        -   `{service_name}`: サービスの名前 (`AtCoder` など)
-   `templates` (table of string): value (右側) のテンプレートによる生成結果を key (左側) で指定したパスに配置する。
    -   default: `{ "main.cpp" = "main.cpp", "main.py" = "main.py", "generate.py" = "generate.py" }`


## License

MIT License
