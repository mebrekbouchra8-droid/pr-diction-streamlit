import streamlit as st

st.set_page_config(page_title="Surveillance bus – Oran", page_icon="🚌")

def evaluer_risque(temp_ext, temp_moteur, liquide_pct, vitesse):
    raisons = []
    score = 0

    if temp_ext >= 38:
        score += 1
        raisons.append("Forte chaleur extérieure")

    if temp_moteur >= 115:
        score += 5
        raisons.append("Température moteur critique")
    elif temp_moteur >= 105:
        score += 2
        raisons.append("Température moteur élevée")

    if liquide_pct < 35:
        score += 3
        raisons.append("Liquide de refroidissement insuffisant")
    elif liquide_pct < 55:
        score += 1
        raisons.append("Niveau de liquide à surveiller")

    if vitesse < 15 and temp_moteur >= 100:
        score += 1
        raisons.append("Circulation lente : refroidissement réduit")

    if score >= 5:
        return "CRITIQUE", raisons
    if score >= 3:
        return "ALERTE", raisons
    return "NORMAL", raisons


st.title("🚌 Détection de surchauffe – Bus à Oran")
st.caption("Simulation pour la route d'Es Sénia durant le mois de juillet.")

col1, col2 = st.columns(2)

with col1:
    temp_ext = st.slider("Température extérieure (°C)", 25, 50, 40)
    temp_moteur = st.slider("Température du moteur (°C)", 70, 130, 100)

with col2:
    liquide_pct = st.slider("Liquide de refroidissement (%)", 0, 100, 70)
    vitesse = st.slider("Vitesse du bus (km/h)", 0, 100, 30)

etat, raisons = evaluer_risque(
    temp_ext, temp_moteur, liquide_pct, vitesse
)

st.divider()
st.subheader(f"État du bus : {etat}")

if etat == "CRITIQUE":
    st.error("Arrêter le bus dans un lieu sûr et appeler immédiatement la maintenance.")
elif etat == "ALERTE":
    st.warning("Réduire la charge du moteur et vérifier rapidement le refroidissement.")
else:
    st.success("Situation normale : poursuivre la surveillance.")

st.write("### Causes détectées")
if raisons:
    for raison in raisons:
        st.write(f"- {raison}")
else:
    st.write("Aucune anomalie détectée.")

st.write("### Données du bus")
st.json({
    "zone": "Route d'Es Sénia, Oran",
    "temperature_exterieure": f"{temp_ext} °C",
    "temperature_moteur": f"{temp_moteur} °C",
    "liquide_refroidissement": f"{liquide_pct} %",
    "vitesse": f"{vitesse} km/h"
})
