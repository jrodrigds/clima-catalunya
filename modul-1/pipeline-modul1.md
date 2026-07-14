def analitza(lat=41.6167, lon=0.6222, data_inici="2000-01-01", data_fi="2025-12-31"):
    import pandas as pd
    import matplotlib.pyplot as plt
    import numpy as np
    
    URL = f"https://archive-api.open-meteo.com/v1/archive?latitude={lat}&longitude={lon}&start_date={data_inici}&end_date={data_fi}&hourly=temperature_2m&timezone=auto&format=csv"
    
    df = pd.read_csv(URL, skiprows=2)
    
    df["time"] = pd.to_datetime(df["time"])
    df["any"] = df["time"].dt.year
    df["mes"] = df["time"].dt.month
    mitjana_temp = df.groupby(["any","mes"])["temperature_2m (°C)"].agg(["mean","min","max"]).reset_index()
    mitjana_temp["temps"] = (mitjana_temp["any"]+ (mitjana_temp["mes"]-1)/12)
    mitjana_any = df.groupby(["any"])["temperature_2m (°C)"].mean().reset_index()
    mitjana_any["temps"] = mitjana_any["any"] + 0.5
    mitjana_periode = mitjana_any["temperature_2m (°C)"].mean()
    desviacio_mitjana = mitjana_any["temperature_2m (°C)"] - mitjana_periode
    pendent, interseccio = np.polyfit(mitjana_any["temps"], mitjana_any["temperature_2m (°C)"], 1)
    taula_resum = df.groupby("any")["temperature_2m (°C)"].agg(["mean","min", "max"]).reset_index()
    taula_resum.to_html(f"ciutat{lat},{lon}_taula.html", index=False)

    plt.figure()
    ax1 = plt.gca()
    ax1.set_title(f"mitjana de temperatura anual de lat={lat} i long={lon} entre les dates {data_inici} i {data_fi}")
    ax1.set_xlabel("Temps (anys)")
    ax2 = plt.twinx()
    ax2.set_ylim(-3,3)
    
    ax1.plot(mitjana_temp["temps"],mitjana_temp["mean"], label='T°C mitjana mensual', color="blue")
    ax2.plot(mitjana_any["temps"], desviacio_mitjana, label='Desviació de T°C mitjana anual vs. mitjana periode', color="red")
    ax1.set_ylabel("Temperatura (°C)", color="blue")
    ax2.axhline(y=0, color="gray", linestyle="--", label=f"T°C mitjana periode = {mitjana_periode.round(2)} °C")
    ax2.set_ylabel("Desviació respecte la mitjana (°C)", color="red")
    ax1.fill_between(mitjana_temp["temps"], mitjana_temp["min"], mitjana_temp["max"], alpha=0.2, color="blue", label="Rang min-max mensual")
    h1, l1 = ax1.get_legend_handles_labels()
    h2, l2 = ax2.get_legend_handles_labels()
    ax1.legend(h1 + h2, l1 + l2, loc='upper center', bbox_to_anchor=(0.5, -0.15), ncol=2)
    plt.savefig(f"ciutat{lat},{lon}.png", dpi=150, bbox_inches="tight")
    
    plt.show()
    print(f"Pendent de la recta de la mitjana de temperatures anuals = {pendent} °C")

    return(taula_resum,pendent)