# 5일차 - Pandas의 강력함에 대해서

데이터 과학자를 위해 테이블형태로 데이터를 다룰 수 있게 해주는 패키지 (python용 엑셀)\
기존 데이터처리 라이브러리인 numpy 대신 주로 사용\
일반인이 데이터분석을 접하기 쉽게 만들어준 결정적인 라이브러리\
pandas만으로도 충분히 데이터 분석이 가능할 정도로 고수준의 함수들을 내장\
앞으로 진행하는 데이터분석 과정에서 주로 사용하게 될 데이터구조

#### 습관적 불러들이기
import numpy as np
#### pandas 로딩
import pandas as pd
#### pd라는 닉네임은 많은 파이썬 유저들이 사용하고 있는 닉네임, 분석을 위한 필수는 아니지만 되도록이면 위와 같이 사용을 해줍시다.
pd.options.display.max_columns = 200 
#### 불러들이는 데이터에 맞춰 모든 컬럼을 확인 가능하도록 옵션값을 주었습니다.
pd.options.display.max_info_columns =200 

2. DataFrame
엑셀에 익숙한 사용자를 위해 제작 된 테이블형태의 데이터 구조
다양한 형태의 데이터를 받아 사용할 수 있으며 다양한 통계, 시각화 함수를 제공한다.

실제 데이터를 불러들이고 값을 확인 해 보며 기본적인 pandas 사용법을 익혀보도록 하겠습니다. 
2-1. 데이터 불러오기
pandas는 다양한 데이터 파일 형태를 지원하며 주로 csv, xlsx, sql을 사용한다.

read_csv()
read_excel()
read_sql()


%%time
# DataFrame 의 약자로서 형식적으로 df 변수명을 사용한다.
# pandas패키지의 read_csv() 함수를 사용하여 loan.csv 파일을 불러들여 데이터프레임을 만들고 df 이름의 변수로 저장

# 주피터 노트북 및 코랩 경로 설정 방법
df = pd.read_csv('./loan1.csv')


%%time
# 만약 모듈을 찾을 수 없는 오류가 발생한다면 추가 모듈 설치
# !pip install xlrd

df = pd.read_excel('loan1.xlsx')

2-2. 데이터 저장하기
불러들인 혹은 작업을 마친 데이터프레임을 다양한 파일형태로 저장이 가능합니다.

to_csv()
to_excel()
to_sql()

%%time
df.to_csv('loan1_test.csv')

%%time
# 엑셀은 오래걸립니다~
df.to_excel('loan1_test.xlsx')


df 
처음 위에 몇개와 아래 몇개의 데이터들을 보여줌

df.head() 위의 5개를 보여주며 key값으로 갯수를 정해줄수 있음
df.tail() 헤드와 마찬가지지만 아래부터 보여줌

# 데이터의 갯수를 살펴봅니다
len(df)

# 데이터의 전반적인 정보를 확인합니다.
df.info()
# dtype 정보에서는 각 컬럼별 데이터 타입을 확인 할 수 있습니다.
# object == str 이라고 생각하셔도 무방합니다.
# verbose, null_counts

데이터 타입 확인은 정말 중요합니다. numpy에서 말했듯이
넘파이배열은 같은 타입만이 같이 존재할 수 있기 때문입니다.

# numpy 함수로 데이터 shape 확인
np.shape(df)

몇 by 몇 행렬인지 확인

# 컬럼
df.columns

존재하는 컬럼 확인 가능

# 인덱스
df.index

인덱스가 몇부터 몇까지 어떤방식으로 존재하는지 확인가능

# 인덱스넘버로 데이터에 접근하는 .iloc[색인]
df.iloc[0]

.iloc으로 인덱스 접근이 가능한것을 꼭 기억해야한다.

# 10번 인덱스 부터 20번 인덱스 샘플 접근
df.iloc[10:20]

# 첫번째 0, 10, 20 인덱스 샘플 접근
df.iloc[[0, 10, 20]]

# 컬럼 단위 샘플 접근
df['emp_title']

정말 많이 사용하는 컬럼단위로 접근이다.

# 여러 컬럼 동시 접근
df[['emp_title', 'grade']]

여러개의 컬럼을 동시에 접근해서 보여준다

# row와 columns을 동시에 슬라이싱 하는 속성
# df.loc[인덱스, 컬럼명]
df.loc[10:20, ['emp_title', 'grade']]

이와 같이 갯수도 정해주어서 사용가능 잘 보고 익힐것 !

df[df['addr_state'] == 'NY']['annual_inc'].mean()

따라서 이런식으로 조건을 주어 평균을 내고 할 수 있다. 미친!!!!

len(df[df['addr_state'] == 'TX'])
df[df['grade'] == 'A']['annual_inc'].mean()

# 신용등급 A와 B인 샘플접근
(df[(df['grade'] == 'A') | (df['grade'] == 'B')]['int_rate'].mean()) - (df[(df['grade'] == 'C') | (df['grade'] == 'D')]['int_rate'].mean())
# 조건식을 여러개 써야 한다면 조건마다 ()로 감싸주시는 것이 좋습니다.

등등 확인 가능

merge_df1 = pd.DataFrame({
    '이름': ['원영', '사쿠라', '유리', '예나', '유진', '나코', '은비', '혜원', '히토미', '채원', '민주', '째욘'],
    '국어': [100, 70, 70, 70, 60, 90, 90, 70, 70, 80, 100, 100],
    '영어': [100, 90, 80, 50, 70, 100, 70, 90, 100, 100, 80, 100]
    }, columns=['이름', '국어', '영어'])

merge_df2 = pd.DataFrame({
    '일어': [80, 100, 100, 90, 70, 50, 100],
    '수학': [90, 70, 100, 80, 70, 80, 90],
    '이름': ['원영', '사쿠라', '나코', '히토미', '예나', '은비', '째욘'],
    }, columns=['일어', '수학', '이름'])

이렇게 데이터 프레임을 만들어 줄 수 있다. 만든 뒤에 이를 csv로
출력하면 되겠다. 크롤링 -> df제작 -> 출력 순 ㄷㄷ...

6. 데이터프레임 병합
실제 분석업무를 진행하다보면 데이터가 여기저기 분산되어 있을 경우가 더 많습니다.
조각난 데이터를 분석에 필요한 데이터셋으로 만들기 위해 데이터프레임 병합을 많이 사용합니다.
한개 이상의 데이터프레임을 병합 할 때 주로 사용하는 함수 2가지를 알아보겠습니다.    
6-1. 데이터 병합에 사용가능한 key(병합할 기준이 되는 행 or 열)값이 있는경우
pd.merge(베이스데이터프레임, 병합할데이터프레임)

6-2. 단순 데이터 연결
pd.concat([베이스데이터프레임, 병합할데이터프레임], axis=0 or 1)

현재 df에 저장되어있는 데이터에 추가로 5만개의 데이터를 이어붙여보겠습니다.
df1이라는 변수에 이어붙일 데이터를 불러들여 병합을 진행해보겠습니다.

# 데이터프레임 행단위 병합
df = pd.concat([df, df1])

df는 이렇게 단순히 병합이 되었다. 물론 df와 df1의 컬럼은 같아야한다.

7. 인덱스 조작
방금 전 concat으로 병합한 데이터프레임의 이상한 점을 찾으셨나요?
데이터 자체는 잘 붙였지만 인덱스가 꼬여있습니다.
인덱스 조작은 데이터분석을 위해 필요한 인덱스를 설정하기 위해 필요합니다.

하지만 위처럼 조작해서 데이터는 늘어났지만 인덱스는 이전 그대로 이기 때문에 수정이 필요하다.

# 인덱스 초기화
df = df.reset_index()
# df

# 기존 컬럼값을 취해 index로 사용
df.set_index('index', inplace=True)

# 기존 인덱스값을 날리면서 인덱스 초기화
df = df.reset_index(drop=True)

이렇게 다시 인덱스를 합친 수로 잘 설정이 가능하다

# df 컬럼명 접근
df.columns

# columns 속성도 인덱싱 및 슬라이싱이 가능합니다.
df.columns[0:26]

# df의 개인정보에 관한 컬럼만을 색인으로 df를 슬라이싱하고 person_df 변수에 바인딩
person_df = df[df.columns[0:26]]
person_df

한마디로 필요한 컬럼의 데이터만 뽑아서 person_df라는 새로운 프레임을 만든것이다.
미친... 정말 엄청난듯하다...

8-1. 컬럼삭제
현재 데이터셋에는 개인식별정보가 지워져서 데이터가 존재하지 않습니다. 불필요한 데이터 column을 지우도록 하겠습니다.

# 지울 column의 데이터값이 모두 NaN인지 확인
person_df['id'].sum(), person_df['member_id'].sum(), person_df['url'].sum(), person_df['desc'].sum()

# 컬럼삭제 drop('컬럼명', axis=1)
# del (df['컬럼명'])
# 실제로는 컬럼 및 행도 삭제 가능합니다. axis=0(기본값)
# inplace=True 파라메터를 사용해서 원본값을 변경가능합니다.
person_df = person_df.drop('id', axis=1)
# person_df = person_df.drop('id', axis=1)

# del 메모리 삭제 키워드 사용
del person_df['url']
del person_df['desc']

8-2. 컬럼명 변경
경우에 따라서는 데이터셋 제작 중 컬럼명을 변경해야 할 경우도 있습니다.
국내 수집 데이터 사용 시 컬럼이 한글일 경우 영어로 변경을 많이 합니다.

# home_ownership을 간략하게 home으로 변경
# 한글도 가능합니다만 권장하지는 않습니다.
person_df.rename(columns={'home_ownership' : 'home'}, inplace=True)


# 값을 카운트 하는 함수 value_counts()
df['emp_title'].value_counts()

같은 값을 가지는 value들을 자동으로 count해서 내림차순으로 보여준다

# Owner, owner 같은 직업이지만 대소문자 구분에 따라 다른 값으로 취급되는 문제가 있네요.
# 대소문자 구분을 없애기 위해 모두 소문자로 데이터값을 변경하겠습니다.
# 소문자 변환 전 혹시모를 int, float 데이터가 있을지 모를 상황에 대비해서 모두 문자열로 변경해주겠습니다.
# 형변환 함수 astype(데이터타입)
df['emp_title'] = df['emp_title'].astype(str)

%%time
# 반복문을 사용한 데이터 변경도 가능
# 하지만 파이썬의 강점을 살리지 못한 코드
for index, title in enumerate(df['emp_title']):
    df['emp_title'][index] = title.lower()

배운사람들의 코드, 고오급 python 스킬
numpy를 학습하면서 브로드캐스팅에 관하여 잠깐 언급했었습니다.
그렇다만 그 파워풀하다던 브로드캐스팅은 어떻게 사용해야할까요?

기타 언어에서는 지원하지 않는 기능이니만큼 파이썬의 특징을 가장 잘 살리는 코드
apply 함수를 사용하여 인자로 받는 모든 데이터에 함수를 적용
간단하게 map()이랑 비슷하다고 생각하면 편하다

apply 함수로 컬럼에 적용시키는 코드 구조
df['컬럼명'] = df['컬럼명'].apply(lambda x: func(x) if 조건문)

>>> # 예
>>> f = lambda x, y : x + y
>>> f(5,6)
11

%%time
# apply() 함수사용 반복이 가능한 데이터구조의 모든 인자에 적용
# lambda 각 인자에 적용할 함수 혹은 연산
df['emp_title'] = df['emp_title'].apply(lambda x: x.lower())


# 컬럼 평균값 계산
df[df['emp_title'] == 'ceo']['annual_inc'].mean()

# 각 직업별 평균연봉이 궁금하다
# 엑셀의 pivol table 과 비슷한 기능
df.groupby('emp_title').mean()

# 위 테이블에서 연간수입 접근
df.groupby('emp_title').mean()['annual_inc']

# 데이터정렬
df.groupby('emp_title').mean()['annual_inc'].sort_values(ascending=False)

이런식으로 정말 어마어마하게 활용되고 무궁무진한 강력한 pandas이다 ....

10. 결측치 처리
데이터 분석을 위해서는 데이터셋 내에 빈 값이 있는 경우 분석에 방해가 될 수 있는 여지가 많습니다.
모든 결측치를 없애야 하는 것은 아니지만 되도록이면 결측치를 채우는 방법, 혹은 없애는 방법등으로 결측치를 처리합니다.
몇가지 예시를 살펴보면서 결측치 처리에 대해 알아봅시다.

# 컬럼별 결측치 확인을 위한 isnull()함수 리턴값이 bool 형태로 반환되어 조건부 샘플링이 가능합니다.
df['emp_title'].isnull().head()

직업과 근속연수에 관한 부분은 데이터를 통한 유추나 계산값을 통해 채워넣을 수 있는 항목은 아닌 것 같습니다.
다만 dti의 경우 실수로 채워져 있는 부분이니 수업을 위해 평균값 혹은 근사치를 계산하여 채워보도록 하겠습니다.

# fillna() 함수로 NaN 값을 dti 컬럼의 평균으로 채우기
df['dti'].fillna(df['dti'].mean(), inplace=True) # inplace 파라메터 사용가능
# fillna() 함수의 다양한 채우기 방법 파라메터 확인해보기
