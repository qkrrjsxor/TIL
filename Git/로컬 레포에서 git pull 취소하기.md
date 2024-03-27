# 로컬 레포지토리에 git pull 취소하기

### 상황
다른 컴퓨터에서 작업하고 push 한것을 sync 하지 않고 작업하여 push 하려다가 오류 발생

### 에러 메세지
```
SSAFY@3▒▒PC143 MINGW64 ~/Desktop/SAM/algorithm (master)
$ git pull origin master
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (7/7), done.     error: There was a problem with the editor 'vi'.lta 2), reused 9 (delta 2), pack-reused 0
Not committing merge; use 'git commit' to complete the merge.
From https://github.com/qkrrjsxor/algorithm
SSAFY@3▒▒PC143 MINGW64 ~/Desktop/SAM/algorithm (master|MERGING)
$
hint: Waiting for your editor to close the file...
SSAFY@3▒▒PC143 MINGW64 ~/Desktop/SAM/algorithm (master|MERGING)
$

SSAFY@3▒▒PC143 MINGW64 ~/Desktop/SAM/algorithm (master|MERGING)
$ git pull origin master
error: You have not concluded your merge (MERGE_HEAD exists).
hint: Please, commit your changes before merging.
fatal: Exiting because of unfinished merge.

```

### 해결 방법
`git reset MERGE_HEAD`