# streamlit, pandas, numpy 라는 마법 도구를 불러올게요.
# 웹사이트를 만들고, 표를 만들고, 숫자를 계산할 때 필요해요.
import streamlit as st
import pandas as pd
import numpy as np

# --- 1. 재미있는 제목과 설명 ---
# 웹페이지 탭에 나올 이름과 전체적인 모양을 정해요.
st.set_page_config(page_title="약들의 달리기 시합!", layout="wide")

# 가장 큰 제목을 써요. 이모지도 넣을 수 있어요!
st.title("우리 몸속 약들의 달리기 시합! 💊💨")
st.write("우리 몸에 약이 들어오면, 몸속 작은 일꾼(효소)들이 약을 가지고 일을 시작해요!")
st.write("약(재료)이 많아질수록 일꾼들은 얼마나 더 빨라질까요? 만약 방해꾼이 나타나면 어떻게 될까요? 함께 알아봐요!")

# --- 2. 달리기 시합 코스 그리기 (그래프) ---
st.header("코스별 달리기 속도 비교! 📊")

# 달리기 시합의 규칙을 정해요.
Vmax = 100  # 일꾼들이 낼 수 있는 최고 속도
Km = 20     # 최고 속도의 절반만큼 빨라지는 데 필요한 약의 양

# 약의 양을 0부터 150까지 정해요. 이게 달리기 코스의 거리가 될 거예요.
S = np.arange(0, 151, 1)

# [코스 1] 아무도 방해하지 않는 평탄한 코스 (억제제 없음)
V_normal = (Vmax * S) / (Km + S)

# [코스 2] 비슷한 친구가 길을 막는 코스 (경쟁적 억제제)
# 결승선(Vmax)에는 도달할 수 있지만, 더 많은 약(S)이 필요해요.
Km_competitive = 40
V_competitive = (Vmax * S) / (Km_competitive + S)

# [코스 3] 일꾼을 직접 방해하는 코스 (비경쟁적 억제제)
# 아무리 약이 많아져도 최고 속도(Vmax)가 낮아져서 빨리 달릴 수 없어요.
Vmax_noncompetitive = 60
V_noncompetitive = (Vmax_noncompetitive * S) / (Km + S)

# 달리기 기록을 표로 만들어요.
chart_data = pd.DataFrame({
    '약의 양': S,
    '쌩쌩 달릴 때': V_normal,
    '길 막힐 때': V_competitive,
    '힘 빠졌을 때': V_noncompetitive
})

# 선 그래프로 달리기 시합을 보여줘요!
st.line_chart(
    chart_data,
    x='약의 양',
    y=['쌩쌩 달릴 때', '길 막힐 때', '힘 빠졌을 때'],
    color=["#0000FF", "#FF8C00", "#FF0000"] # 파란색, 주황색, 빨간색 선
)
st.info("파란선은 아무 방해 없이 달릴 때, 주황선은 **다른 약이 길을 막을 때**, 빨간선은 **일꾼이 힘이 빠졌을 때**의 속도예요. 정말 다르죠?")


# --- 3. 어떤 코스가 가장 신기한가요? (투표하기) ---
st.header("어떤 달리기 코스가 가장 신기한가요? 🤔")

# 투표 결과를 저장할 비밀 상자를 만들어요.
if 'votes' not in st.session_state:
    st.session_state['votes'] = {'쌩쌩 달릴 때': 0, '길 막힐 때': 0, '힘 빠졌을 때': 0}

# 'form'으로 투표 용지를 만들어요.
with st.form("vote_form"):
    st.write("그래프를 보고 가장 신기하거나 재미있는 코스에 투표해주세요!")
    
    # 여러 개 중에 하나를 고를 수 있는 버튼을 만들어요.
    vote_option = st.radio(
        "투표할 코스를 골라주세요:",
        ('쌩쌩 달릴 때', '길 막힐 때', '힘 빠졌을 때')
    )
    
    # '투표하기' 버튼을 만들어요.
    submitted = st.form_submit_button("여기를 눌러 투표하기!")
    
    # 만약 버튼을 누르면,
    if submitted:
        # 내가 고른 코스의 투표 수를 1 늘려줘요.
        st.session_state.votes[vote_option] += 1
        st.success(f"'{vote_option}' 코스에 투표했어요. 고마워요!") # 투표 완료 메시지

# --- 4. 실시간 투표 결과 보기 ---
st.header("친구들의 투표 결과는? 🗳️")

# 투표 결과를 표로 바꿔요.
vote_counts = st.session_state.votes
vote_df = pd.DataFrame(list(vote_counts.items()), columns=['달리기 코스', '투표 수'])

# 막대그래프로 어떤 코스가 인기가 많은지 보여줘요.
st.bar_chart(vote_df.set_index('달리기 코스'))

st.write("다른 친구들은 어떤 코스를 가장 신기하게 생각하는지 바로바로 볼 수 있어요!")
