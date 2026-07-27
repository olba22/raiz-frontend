[raiz-motorista.html](https://github.com/user-attachments/files/30396838/raiz-motorista.html)
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>RAIZ — Pide un motorista</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --naranja: #FF6B00; --negro: #0A0A0A; --gris-osc: #111111;
      --gris-card: #161616; --gris-brd: #222222; --blanco: #F5F5F5;
      --texto-sec: #888888; --verde: #1DB954;
    }
    body { font-family: 'Inter', sans-serif; background: var(--negro); color: var(--blanco); max-width: 480px; margin: 0 auto; min-height: 100vh; }
    .top {
      padding: 1.25rem; display: flex; align-items: center; gap: .75rem;
      border-bottom: 1px solid var(--gris-brd);
    }
    .top-back {
      width: 36px; height: 36px; border-radius: 10px; background: var(--gris-card);
      border: 1px solid var(--gris-brd); color: var(--blanco); font-size: 1rem;
      display: flex; align-items: center; justify-content: center; cursor: pointer; text-decoration: none;
    }
    .top-title { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.05rem; }
    .hero { padding: 1.5rem 1.25rem 0; text-align: center; }
    .hero-icon { font-size: 2.4rem; margin-bottom: .5rem; }
    .hero h1 { font-family: 'Syne', sans-serif; font-size: 1.4rem; font-weight: 800; margin-bottom: .4rem; }
    .hero p { color: var(--texto-sec); font-size: .88rem; line-height: 1.5; max-width: 360px; margin: 0 auto; }

    .form-wrap { padding: 1.5rem 1.25rem; }
    .campo { margin-bottom: 1rem; }
    .campo label { display: block; font-size: .8rem; font-weight: 600; margin-bottom: .4rem; }
    .campo label span { color: var(--naranja); }
    .input {
      width: 100%; background: var(--gris-card); border: 1px solid var(--gris-brd);
      border-radius: 10px; padding: .75rem .9rem; font-size: .9rem;
      color: var(--blanco); font-family: 'Inter', sans-serif; outline: none; transition: border-color .2s;
    }
    .input:focus { border-color: var(--naranja); }
    .input::placeholder { color: var(--texto-sec); }
    textarea.input { resize: vertical; min-height: 70px; }
    .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: .8rem; }
    .btn-solicitar {
      width: 100%; background: var(--naranja); color: var(--negro);
      border: none; border-radius: 12px; cursor: pointer;
      padding: 1rem; font-size: .95rem; font-weight: 700;
      font-family: 'Inter', sans-serif; margin-top: .5rem; transition: background .2s;
    }
    .btn-solicitar:hover { background: #ff8533; }
    .btn-solicitar:disabled { opacity: .6; cursor: not-allowed; }
    #formMensaje { font-size: .85rem; color: var(--texto-sec); margin-top: .75rem; text-align: center; }

    /* ESTADO DE ESPERA / CONFIRMACIÓN */
    .estado-wrap { display: none; padding: 2.5rem 1.5rem; text-align: center; }
    .estado-wrap.show { display: block; }
    .spinner {
      width: 46px; height: 46px; border-radius: 50%;
      border: 3px solid var(--gris-brd); border-top-color: var(--naranja);
      margin: 0 auto 1.25rem; animation: girar 1s linear infinite;
    }
    @keyframes girar { to { transform: rotate(360deg); } }
    .estado-wrap h2 { font-family: 'Syne', sans-serif; font-size: 1.15rem; font-weight: 800; margin-bottom: .5rem; }
    .estado-wrap p { color: var(--texto-sec); font-size: .88rem; line-height: 1.5; }
    .conductor-card {
      margin-top: 1.5rem; background: var(--gris-card); border: 1px solid var(--verde);
      border-radius: 16px; padding: 1.25rem; text-align: left; display: none;
    }
    .conductor-card.show { display: block; }
    .conductor-row { display: flex; align-items: center; gap: .85rem; margin-bottom: 1rem; }
    .conductor-avatar {
      width: 48px; height: 48px; background: var(--naranja); border-radius: 50%;
      display: flex; align-items: center; justify-content: center; font-size: 1.4rem; flex-shrink: 0;
    }
    .conductor-info strong { display: block; font-size: .95rem; font-weight: 700; }
    .conductor-info span { font-size: .8rem; color: var(--texto-sec); }
    .btn-contactar {
      width: 100%; background: var(--verde); color: var(--negro);
      border: none; border-radius: 10px; cursor: pointer;
      padding: .8rem; font-size: .9rem; font-weight: 700;
      font-family: 'Inter', sans-serif; text-decoration: none; display: block; text-align: center;
    }
    .btn-nueva {
      width: 100%; background: transparent; color: var(--texto-sec);
      border: 1px solid var(--gris-brd); border-radius: 10px; cursor: pointer;
      padding: .75rem; font-size: .85rem; font-weight: 600;
      font-family: 'Inter', sans-serif; margin-top: 1rem;
    }
  </style>
</head>
<body>

<div class="top">
  <a class="top-back" href="/raiz.html">←</a>
  <div class="top-title">🛵 Pide un motorista</div>
</div>

<!-- FORMULARIO -->
<div id="pantallaForm">
  <div class="hero">
    <div class="hero-icon">🛵</div>
    <h1>¿A dónde vas o qué necesitas mandar a hacer?</h1>
    <p>Tu solicitud se envía a todos los motoristas disponibles de tu zona — el primero que la acepte te contacta por WhatsApp.</p>
  </div>

  <div class="form-wrap">
    <div class="campo">
      <label>¿Qué necesitas? <span>*</span></label>
      <textarea class="input" id="motoDescripcion" placeholder="Ej: Llevarme de mi casa al hospital, o comprarme un medicamento en la farmacia..."></textarea>
    </div>
    <div class="campo">
      <label>Punto de origen <span>*</span></label>
      <input class="input" id="motoOrigen" type="text" placeholder="Ej: Calle Duarte #12" />
    </div>
    <div class="campo">
      <label>Punto de destino</label>
      <input class="input" id="motoDestino" type="text" placeholder="Ej: Hospital Municipal (déjalo vacío si no aplica)" />
    </div>
    <div class="grid2">
      <div class="campo">
        <label>Municipio <span>*</span></label>
        <input class="input" id="motoMunicipio" type="text" placeholder="Ej: Pedernales" />
      </div>
      <div class="campo">
        <label>Provincia <span>*</span></label>
        <input class="input" id="motoProvincia" type="text" placeholder="Ej: Pedernales" />
      </div>
    </div>
    <div class="grid2">
      <div class="campo">
        <label>Tu nombre <span>*</span></label>
        <input class="input" id="motoNombre" type="text" placeholder="Ej: Ana Ramírez" />
      </div>
      <div class="campo">
        <label>Tu WhatsApp <span>*</span></label>
        <input class="input" id="motoWhatsapp" type="tel" placeholder="8095551234" />
      </div>
    </div>
    <div class="campo">
      <label>¿Cuánto ofreces por el servicio? (RD$)</label>
      <input class="input" id="motoOferta" type="number" placeholder="100" value="100" />
    </div>

    <button class="btn-solicitar" id="btnSolicitar" onclick="solicitarMotorista()">🛵 Enviar solicitud a los motoristas</button>
    <div id="formMensaje"></div>
  </div>
</div>

<!-- ESTADO DE ESPERA / CONFIRMACIÓN -->
<div class="estado-wrap" id="pantallaEstado">
  <div class="spinner" id="spinnerBuscando"></div>
  <h2 id="estadoTitulo">Buscando un motorista cerca de ti...</h2>
  <p id="estadoTexto">Tu solicitud ya está viajando a todos los motoristas disponibles en tu zona. Esto puede tomar unos minutos.</p>

  <div class="conductor-card" id="conductorCard">
    <div class="conductor-row">
      <div class="conductor-avatar" id="conductorAvatar">🛵</div>
      <div class="conductor-info">
        <strong id="conductorNombre">—</strong>
        <span>Va en camino a atenderte</span>
      </div>
    </div>
    <a class="btn-contactar" id="btnContactarConductor" href="#" target="_blank">💬 Contactar por WhatsApp</a>
  </div>

  <button class="btn-nueva" onclick="reiniciarFormulario()">← Hacer otra solicitud</button>
</div>

<script>
  const API = 'https://raiz-backend.onrender.com';
  let solicitudIdActual = null;
  let pollEstadoInterval = null;

  async function solicitarMotorista() {
    const descripcion = document.getElementById('motoDescripcion').value.trim();
    const origen = document.getElementById('motoOrigen').value.trim();
    const destino = document.getElementById('motoDestino').value.trim();
    const municipio = document.getElementById('motoMunicipio').value.trim();
    const provincia = document.getElementById('motoProvincia').value.trim();
    const nombre = document.getElementById('motoNombre').value.trim();
    const whatsapp = document.getElementById('motoWhatsapp').value.trim();
    const oferta = parseFloat(document.getElementById('motoOferta').value) || 0;
    const mensaje = document.getElementById('formMensaje');

    if (!descripcion || !origen || !municipio || !provincia || !nombre || !whatsapp) {
      mensaje.textContent = '⚠️ Completa qué necesitas, origen, municipio, provincia, tu nombre y tu WhatsApp.';
      return;
    }

    const btn = document.getElementById('btnSolicitar');
    btn.disabled = true;
    btn.textContent = 'Enviando...';
    mensaje.textContent = '';

    try {
      const res = await fetch(`${API}/solicitudes-delivery`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          tipo: 'diligencia',
          municipio, provincia,
          cliente_nombre: nombre,
          cliente_whatsapp: whatsapp,
          origen_texto: origen,
          destino_texto: destino || null,
          descripcion,
          costo_delivery: oferta
        })
      });
      const data = await res.json();
      if (!res.ok) {
        mensaje.textContent = '⚠️ ' + (data.detail || 'No se pudo enviar la solicitud. Intenta de nuevo.');
        btn.disabled = false;
        btn.textContent = '🛵 Enviar solicitud a los motoristas';
        return;
      }
      solicitudIdActual = data.id;
      document.getElementById('pantallaForm').style.display = 'none';
      document.getElementById('pantallaEstado').classList.add('show');
      iniciarConsultaEstado();
    } catch (e) {
      mensaje.textContent = '⚠️ No se pudo conectar con el servidor.';
      btn.disabled = false;
      btn.textContent = '🛵 Enviar solicitud a los motoristas';
    }
  }

  function iniciarConsultaEstado() {
    detenerConsultaEstado();
    consultarEstado();
    pollEstadoInterval = setInterval(consultarEstado, 5000);
  }
  function detenerConsultaEstado() {
    if (pollEstadoInterval) clearInterval(pollEstadoInterval);
    pollEstadoInterval = null;
  }

  async function consultarEstado() {
    if (!solicitudIdActual) return;
    try {
      const res = await fetch(`${API}/solicitudes-delivery/${solicitudIdActual}`);
      if (!res.ok) return;
      const s = await res.json();
      if (s.conductor_id) {
        detenerConsultaEstado();
        mostrarConductorAsignado(s);
      }
    } catch (e) { /* se reintenta en el próximo ciclo */ }
  }

  function mostrarConductorAsignado(s) {
    document.getElementById('spinnerBuscando').style.display = 'none';
    document.getElementById('estadoTitulo').textContent = '✅ ¡Un motorista aceptó tu solicitud!';
    document.getElementById('estadoTexto').textContent = 'Contáctalo por WhatsApp para coordinar los detalles.';
    document.getElementById('conductorAvatar').textContent = s.conductor_emoji || '🛵';
    document.getElementById('conductorNombre').textContent = s.conductor_nombre || 'Motorista';
    const whatsapp = (s.conductor_whatsapp || '').replace(/\D/g, '');
    const mensajeWa = encodeURIComponent(`🌱 Hola, te contacto por mi solicitud en RAIZ: "${s.descripcion}"`);
    document.getElementById('btnContactarConductor').href = `https://wa.me/${whatsapp}?text=${mensajeWa}`;
    document.getElementById('conductorCard').classList.add('show');
  }

  function reiniciarFormulario() {
    detenerConsultaEstado();
    solicitudIdActual = null;
    document.getElementById('pantallaEstado').classList.remove('show');
    document.getElementById('conductorCard').classList.remove('show');
    document.getElementById('spinnerBuscando').style.display = 'block';
    document.getElementById('estadoTitulo').textContent = 'Buscando un motorista cerca de ti...';
    document.getElementById('estadoTexto').textContent = 'Tu solicitud ya está viajando a todos los motoristas disponibles en tu zona. Esto puede tomar unos minutos.';
    document.getElementById('motoDescripcion').value = '';
    document.getElementById('motoOrigen').value = '';
    document.getElementById('motoDestino').value = '';
    document.getElementById('formMensaje').textContent = '';
    document.getElementById('btnSolicitar').disabled = false;
    document.getElementById('btnSolicitar').textContent = '🛵 Enviar solicitud a los motoristas';
    document.getElementById('pantallaForm').style.display = 'block';
  }
</script>
</body>
</html>
