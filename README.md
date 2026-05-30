# Huffman
# Huffman 文件压缩工具 — 使用指南
1.打开命令行，在 `huffman_fixed` 文件夹的**地址栏**输入 `cmd`，回车：
2.在黑窗口里逐行复制执行下面命令：

```cmd
 1. 创建测试文件
echo 霍夫曼编码是David Huffman在1952年提出的一种变长编码方法。> test.txt
echo 它通过统计字符出现频率，给高频字符分配短编码，低频字符分配长编码。>> test.txt
echo 这样可以大大减少文件的总比特数，实现数据压缩。>> test.txt

2. 压缩
huff -c test.txt -o demo.huff

3. 解压
huff -x demo.huff -d result

4. 验证（比较原文件和解压文件是否一致）
fc test.txt result\test.txt
```

如果最后显示 **"找不到相异处"** 或 **"FC: 找不到差异"**，说明压缩解压成功


3.测试通配符 *

```cmd
创建多个文件
mkdir files
echo AAA > files\a.txt
echo BBBBB > files\b.txt
echo CCC > files\c.txt
echo 不匹配 > files\d.ini

只压缩 .txt（*.txt 会自动匹配 a.txt b.txt c.txt）
huff -c "files\*.txt" -o wildcard.huff

解压
huff -x wildcard.huff -d wildcard_out
 检查 d.ini 是否被正确排除（应该不在 wildcard_out 里）
dir wildcard_out
```

4. 测试通配符 ?
```cmd
? 匹配恰好一个字符
huff -c "files\?.txt" -o single.huff
结果：a.txt c.txt（b.txt 名字太长不匹配）
```
