# Linux 필수 명령어 18가지
### 1. ls (List files and directories) - 파일과 디렉토리 목록 표시
현재 디렉토리의 파일과 폴더 목록을 보여주는 기본 명령어
```bashCopy
# 기본 사용
ls
# 상세 정보 표시
ls -l
# 숨김 파일 포함하여 상세 정보 표시
ls -la
```

### 2. cd (Change directory) - 디렉토리 이동

현재 작업 디렉토리를 변경하는 명령어

```bashCopy
# 홈 디렉토리로 이동
cd ~
# 상위 디렉토리로 이동
cd ..
# 특정 경로로 이동
cd /var/log
```


### 3. mkdir (Make directory) - 새 디렉토리 생성

새로운 디렉토리를 생성하는 명령어

```bashCopy
# 단일 디렉토리 생성
mkdir test
# 다중 디렉토리 생성
mkdir test1 test2
# 하위 디렉토리까지 한 번에 생성
mkdir -p test/subdir1/subdir2
```

### 4. rm (Remove) - 파일 또는 디렉토리 삭제

파일이나 디렉토리를 삭제하는 명령어

```bashCopy
# 파일 삭제
rm file.txt
# 디렉토리와 그 내용 모두 삭제
rm -r directory
# 강제 삭제 (확인 없이)
rm -rf directory
```

### 5. mv (Move) - 파일 이동 또는 이름 변경

파일을 이동하거나 이름을 변경하는 명령어

```bashCopy
# 파일 이름 변경
mv oldname.txt newname.txt
# 파일 이동
mv file.txt /home/user/Documents/
# 여러 파일을 디렉토리로 이동
mv file1.txt file2.txt directory/
```

### 6. chmod (Change mode) - 파일 권한 변경

파일이나 디렉토리의 접근 권한을 변경하는 명령어

```bashCopy
# 숫자를 사용한 권한 변경
chmod 755 file.txt
# 문자를 사용한 권한 변경
chmod u+x script.sh
# 재귀적으로 디렉토리 권한 변경
chmod -R 644 directory/
```

```bash
# 777 (rwxrwxrwx): 모든 사용자에게 모든 권한
chmod 777 file.txt

# 755 (rwxr-xr-x): 소유자는 모든 권한, 그룹과 기타 사용자는 읽기와 실행
chmod 755 file.txt

# 644 (rw-r--r--): 소유자는 읽기와 쓰기, 그룹과 기타 사용자는 읽기만
chmod 644 file.txt

# 700 (rwx------): 소유자만 모든 권한, 다른 사용자는 권한 없음
chmod 700 file.txt

# 666 (rw-rw-rw-): 모든 사용자에게 읽기와 쓰기 권한
chmod 666 file.txt
```

### 7. cp (Copy) - 파일 복사

파일이나 디렉토리를 복사하는 명령어

```bashCopy
# 파일 복사
cp source.txt destination.txt
# 디렉토리 복사
cp -r sourcedir/ destdir/
# 속성 유지하며 복사
cp -p file.txt backup/
```

### 8. find - 파일 검색

파일이나 디렉토리를 검색하는 명령어

```bashCopy
# 이름으로 검색
find /home -name "*.txt"
# 크기로 검색 (100MB보다 큰 파일)
find / -size +100M
# 최근 7일 내에 수정된 파일
find . -mtime -7
```


### 9. grep - 파일 내용 검색

파일 내에서 특정 패턴이나 문자열을 검색하는 명령어

```bashCopy
# 기본 검색
grep "pattern" file.txt
# 재귀적으로 모든 파일에서 검색
grep -r "pattern" directory/
# 대소문자 구분 없이 검색
grep -i "pattern" file.txt
```


### 10. vi - 텍스트 편집기

기본적인 텍스트 편집기

```bashCopy
# 파일 열기
vi file.txt
# 주요 명령어
# i: 입력 모드
# :w: 저장
# :q: 종료
# :wq: 저장 후 종료
```


### 11. cat (Concatenate) - 파일 내용 표시

파일의 내용을 화면에 표시하는 명령어

```bashCopy
# 파일 내용 보기
cat file.txt
# 여러 파일 연결해서 보기
cat file1.txt file2.txt
# 행 번호 표시
cat -n file.txt
```


### 12. tar - 파일 압축 및 해제

여러 파일을 하나의 아카이브로 묶거나 푸는 명령어

```bashCopy
# 파일 압축하기
tar -czvf archive.tar.gz directory/
# 압축 해제하기
tar -xzvf archive.tar.gz
# 압축 파일 내용 보기
tar -tvf archive.tar.gz
```


### 13. ps (Process Status) - 프로세스 정보 표시

실행 중인 프로세스 목록과 상태를 보여주는 명령어

```bashCopy
# 모든 프로세스 보기
ps aux
# 특정 사용자의 프로세스 보기
ps -u username
# 프로세스 트리 보기
ps axjf
```


### 14. kill - 프로세스 종료

실행 중인 프로세스를 종료하는 명령어

```bashCopy
# 프로세스 종료
kill 1234
# 강제 종료
kill -9 1234
# 프로세스 이름으로 종료
killall firefox
```


### 15. top - 시스템 자원 사용 현황

시스템의 프로세스와 자원 사용률을 실시간으로 모니터링
실행 중 사용할 수 있는 명령어:

```bashCopy
# 기본 실행
top
# 실행 중 사용할 수 있는 키
# M: 메모리 사용률 순 정렬
# P: CPU 사용률 순 정렬
# q: 종료
```

### 16. ifconfig - 네트워크 인터페이스 설정

네트워크 인터페이스의 설정을 확인하고 변경하는 명령어

```bashCopy
# 모든 인터페이스 정보 보기
ifconfig
# 특정 인터페이스 정보
ifconfig eth0
# IP 주소 설정
ifconfig eth0 192.168.1.100
```

17. ping - 네트워크 연결 테스트
네트워크 호스트와의 연결 상태를 테스트하는 명령어
```bashCopy
# 기본 사용
ping google.com
# 횟수 제한
ping -c 4 google.com
# 간격 설정 (초 단위)
ping -i 2 google.com
```

18. du (Disk Usage) - 디스크 사용량 확인
파일과 디렉토리의 디스크 사용량을 확인하는 명령어
```bashCopy
# 현재 디렉토리 사용량
du -h
# 특정 디렉토리 사용량
du -sh /home
# 상위 10개 큰 디렉토리 찾기
du -h | sort -rh | head -10
```