import streamlit as st

st.title("🤖 Mini Akinator Demo")
st.write("Think of an animal and I will try to guess it!")

# Session state to store answers
if "step" not in st.session_state:
    st.session_state.step = 0

questions = [
    "Is it a pet?",
    "Is it larger than a human?",
    "Does it live in water?",
]

# Ask questions step by step
if st.session_state.step < len(questions):
    answer = st.radio(questions[st.session_state.step], ["Yes", "No"])
    if st.button("Next"):
        st.session_state[f"q{st.session_state.step}"] = answer
        st.session_state.step += 1
        st.experimental_rerun()
else:
    # Simple logic to guess
    q0 = st.session_state.get("q0")
    q1 = st.session_state.get("q1")
    q2 = st.session_state.get("q2")

    if q0 == "Yes" and q2 == "No":
        guess = "a Dog 🐶"
    elif q0 == "Yes" and q2 == "Yes":
        guess = "a Fish 🐠"
    elif q0 == "No" and q1 == "Yes":
        guess = "an Elephant 🐘"
    elif q0 == "No" and q2 == "Yes":
        guess = "a Shark 🦈"
    else:
        guess = "a Bird 🐦"

    st.subheader(f"My guess is... **{guess}**!")
    if st.button("Play Again"):
        st.session_state.clear()
        st.experimental_rerun()
