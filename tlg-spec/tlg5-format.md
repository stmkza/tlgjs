# TLG5 ファイルフォーマット
```
ファイルヘッダ [11bytes]
    (char*6)    #"TLG5.0"
    (u8)        #00
    (char*3)    #"raw"
    (u8)        #1a

画像情報
    (u8)        Color count
                    #03 : RGB
                    #04 : RGBA
    (i32LE)     Width
    (i32LE)     Height
    (i32LE)     Block height (圧縮するときの縦方向の分割単位)

// Block countの求め方
// floor((Height - 1) / Block height) + 1

圧縮ブロックサイズ [4*(Block count)]
    (i32LE)     Block size
    [...圧縮ブロックサイズの繰り返し...]

圧縮された画像データ
    圧縮ブロック
        (u8)        Compress flag
                        #00 : Compressed
                        #01 : Not compressed
        (i32LE)     Block content size
        ブロック本体 [(Block content size) bytes]
```
