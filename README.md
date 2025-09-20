# dash.
import streamlit as st
import pandas as pd


st.title("Calculadora de médias de notas")

st.subheader("Insira as notas das matérias")

materias = ["português", "matematica", "fisica", "quimica", "biologia", "historia", "geografia", "ingles"]
notas = []

for materia in materias:
    nota = st.number_input(f"Nota de {materia}", min_value=0.0, max_value=10.0, step=0.1)
    notas.append(nota)

if st.button("Calcular Média"):
    df = pd.DataFrame({
        "Matérias": materias,
        "Notas": notas
    })

    media = df["Notas"].mean()

    st.subheader("Boletim")
    st.dataframe(df)

    st.write(f"Média Geral é: {media:.2f}")

    if st.button("Salvar em Excel"):
        df.to_excel("boletim.xlsx", index=False, engine="openpyxl")
        st.success("Boletim salvo como 'boletim.xlsx'")


