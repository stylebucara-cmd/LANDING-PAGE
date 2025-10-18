import React from "react";
import { Phone, MessageCircle, Clock, Shield, MapPin, Truck, ChevronRight, CheckCircle2 } from "lucide-react";

// === Moto Style Logo (SVG) ===
const COLORS = { blue: "#1E90FF", orange: "#FF6B00", white: "#FFFFFF" };
function MotoLogo({ variant = "mark", className = "h-10 w-10" }: { variant?: "mark" | "stacked"; className?: string }) {
  const Icon = (
    <svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" className="h-full w-full">
      {/* Ruedas */}
      <circle cx="18" cy="46" r="8" fill={COLORS.white} stroke={COLORS.blue} strokeWidth="3" />
      <circle cx="46" cy="46" r="8" fill={COLORS.white} stroke={COLORS.blue} strokeWidth="3" />
      {/* Marco moto minimal derecha */}
      <path d="M22 40h8l8-10h8" fill="none" stroke={COLORS.blue} strokeWidth="3" strokeLinecap="round" strokeLinejoin="round" />
      <path d="M30 30l6 6" fill="none" stroke={COLORS.blue} strokeWidth="3" strokeLinecap="round" />
      {/* Manubrio / faro */}
      <path d="M46 30h6" stroke={COLORS.orange} strokeWidth="3" strokeLinecap="round" />
      {/* Asiento */}
      <path d="M28 34h6" stroke={COLORS.blue} strokeWidth="3" strokeLinecap="round" />
    </svg>
  );

  if (variant === "stacked") {
    return (
      <div className={`inline-flex flex-col items-center ${className}`}>
        <div className="h-16 w-16 rounded-2xl bg-white shadow grid place-items-center">{Icon}</div>
        <div className="mt-2 text-center leading-tight">
          <div className="text-[10px] font-extrabold tracking-widest" style={{ color: COLORS.blue }}>MOTO STYLE</div>
          <div className="text-[9px] font-bold tracking-wide" style={{ color: COLORS.orange }}>MENSAJERÍA</div>
        </div>
      </div>
    );
  }

  // Mark (solo ícono cuadrado)
  return (
    <div className={`grid ${className} place-items-center rounded-xl bg-white shadow`}>{Icon}</div>
  );
}


// === Simple helpers ===
const Container = ({ children }: { children: React.ReactNode }) => (
  <div className="mx-auto w-full max-w-6xl px-4 sm:px-6 lg:px-8">{children}</div>
);

const SectionTitle = ({ eyebrow, title, subtitle }: { eyebrow?: string; title: string; subtitle?: string }) => (
  <div className="mx-auto max-w-2xl text-center">
    {eyebrow && <p className="text-sm font-semibold uppercase tracking-widest text-blue-600">{eyebrow}</p>}
    <h2 className="mt-2 text-3xl font-extrabold tracking-tight text-gray-900 sm:text-4xl">{title}</h2>
    {subtitle && <p className="mt-3 text-base text-gray-600">{subtitle}</p>}
  </div>
);

// === Theme / brand quick edits ===
const BRAND = {
  name: "Moto Style Mensajería",
  phone: "+57 318 331 1111",
  phoneHref: "tel:+573183311111",
  whatsappHref: "https://wa.me/573183311111",
  primary: "orange-500", // tailwind color token (no #)
  dark: "gray-900",
};

const PrimaryBtn = ({ href, children, as = "a" as const }: { href?: string; children: React.ReactNode; as?: any }) => {
  const common = "inline-flex items-center gap-2 rounded-2xl px-5 py-3 text-base font-semibold shadow-sm hover:shadow transition";
  const className = `bg-${BRAND.primary} text-black hover:brightness-95 ${common}`;
  const Comp = as;
  return <Comp href={href} className={className}>{children}</Comp>;
};

const OutlineBtn = ({ href, children }: { href?: string; children: React.ReactNode }) => (
  <a href={href} className="inline-flex items-center gap-2 rounded-2xl border border-gray-300 px-5 py-3 text-base font-semibold text-gray-800 hover:bg-gray-50 transition">
    {children}
  </a>
);

function Hero() {
  return (
    <div
      className="relative isolate overflow-hidden"
      style={{
        backgroundImage:
          'url("https://source.unsplash.com/1600x900/?bucaramanga,city")',
        backgroundSize: 'cover',
        backgroundPosition: 'center',
      }}
    >
      <div className="absolute inset-0 bg-black/50" />
      <Container>
        <div className="relative z-10 grid items-center gap-10 py-20 lg:grid-cols-2">
          <div className="text-white">
            <p className="mb-3 inline-flex items-center gap-2 rounded-full border border-white/30 bg-white/10 px-3 py-1 text-xs font-semibold">
              <CheckCircle2 className="h-4 w-4 text-green-400" /> Entregas el mismo día en AMB
            </p>
            <h1 className="text-4xl font-extrabold tracking-tight sm:text-6xl">
              Mensajería exprés en <span className="text-blue-300">Bucaramanga</span>
            </h1>
            <p className="mt-4 text-lg leading-7 text-white/90">
              {BRAND.name} recoge y entrega tus envíos en Bucaramanga, Floridablanca, Girón y Piedecuesta. Pide tu domicilio ya por WhatsApp. Servicio inmediato en Bucaramanga y el área metropolitana.
            </p>
            <div className="mt-8 flex flex-wrap items-center gap-3">
              <a href={BRAND.whatsappHref} className={`inline-flex items-center gap-2 rounded-2xl bg-${BRAND.primary} px-6 py-3 text-base font-semibold text-black shadow-lg hover:brightness-95`}>
                <MessageCircle className="h-5 w-5" /> Escribir por WhatsApp
              </a>
              <a href={BRAND.phoneHref} className="inline-flex items-center gap-2 rounded-2xl border border-white/30 bg-white/10 px-6 py-3 text-base font-semibold text-white hover:bg-white/20">
                <Phone className="h-5 w-5" /> Llamar {BRAND.phone}
              </a>
            </div>
            <div className="mt-6 grid max-w-md grid-cols-2 gap-4 text-sm text-white/90">
              <div className="flex items-center gap-2"><Clock className="h-4 w-4" /> 7:00am – 9:00pm</div>
              <div className="flex items-center gap-2"><Shield className="h-4 w-4" /> Seguro básico</div>
            </div>
          </div>
          <div className="relative">
            <div className="rounded-3xl border border-white/20 bg-white/10 p-2 shadow-2xl backdrop-blur">
              <img
                className="h-[360px] w-full rounded-2xl object-cover"
                src="https://images.unsplash.com/photo-1502877338535-766e1452684a?q=80&w=1600&auto=format&fit=crop"
                alt="Mensajero en moto entregando paquetes"
              />
            </div>
            <div className="pointer-events-none absolute -bottom-4 left-6 right-6 h-24 rounded-3xl bg-gradient-to-t from-black/30 to-transparent" />
          </div>
        </div>
      </Container>
      <svg className="absolute inset-x-0 -bottom-24 -z-10 h-72 w-[200%] translate-y-1/2 fill-blue-100" viewBox="0 0 1155 678" preserveAspectRatio="none" aria-hidden="true">
        <path d="M317.219 518.975L203.852 678 0 505.591V0h1155v505.591l-214.507 173.482-221.934-318.87-401.34 158.772z" />
      </svg>
    </div>
  );
}

function Services() {
  const items = [
    { icon: <Truck className="h-5 w-5" />, title: "Envíos exprés", desc: "Entrega en horas dentro de la ciudad." },
    { icon: <MapPin className="h-5 w-5" />, title: "Mensajería urbana", desc: "Documentos, paquetes y compras urgentes." },
    { icon: <Shield className="h-5 w-5" />, title: "Pagos contraentrega", desc: "Cobra a tu cliente al momento de entregar." },
    { icon: <Clock className="h-5 w-5" />, title: "Rutas programadas", desc: "Recolecciones diarias o semanales para negocios." },
  ];
  return (
    <section className="py-16 sm:py-20">
      <Container>
        <SectionTitle eyebrow="Servicios" title="Lo que hacemos" subtitle="Soluciones de mensajería para personas y negocios" />
        <div className="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
          {items.map((it) => (
            <div key={it.title} className="group rounded-3xl border bg-white p-6 shadow-sm transition hover:shadow-lg">
              <div className={`mb-4 inline-flex rounded-2xl bg-${BRAND.primary}/10 p-3`}>{it.icon}</div>
              <h3 className="text-lg font-semibold text-gray-900">{it.title}</h3>
              <p className="mt-1 text-sm text-gray-600">{it.desc}</p>
              <a href={BRAND.whatsappHref} className="mt-4 inline-flex items-center text-sm font-semibold text-gray-900">
                Cotizar ahora <ChevronRight className="ml-1 h-4 w-4" />
              </a>
            </div>
          ))}
        </div>
      </Container>
    </section>
  );
}

function Pricing() {
  const tiers = [
    { name: "Dentro de Bucaramanga", price: "$6.000 – $8.000", features: ["Zonas urbanas", "Paquetes pequeños", "Seguimiento por WhatsApp"] },
    { name: "B/manga – Florida / Girón", price: "$12.000 – $16.000", features: ["Intermunicipal corto", "Entrega segura", "Prueba de entrega con foto"] },
    { name: "B/manga – Piedecuesta", price: "$20.000 – $28.000", features: ["Recorrido largo", "Tarifa según distancia", "Opciones empresariales"] },
  ];
  return (
    <section className="bg-gray-50 py-16 sm:py-20">
      <Container>
        <SectionTitle eyebrow="Tarifas" title="Precios transparentes" subtitle="Cotiza tu envío en segundos por WhatsApp" />
        <div className="mt-10 grid gap-6 lg:grid-cols-3">
          {tiers.map((t) => (
            <div key={t.name} className="rounded-3xl border bg-white p-6 shadow-sm">
              <h3 className="text-xl font-bold text-gray-900">{t.name}</h3>
              <p className="mt-2 text-3xl font-extrabold text-gray-900">{t.price}</p>
              <ul className="mt-4 space-y-2 text-sm text-gray-700">
                {t.features.map((f) => (
                  <li key={f} className="flex items-center gap-2"><CheckCircle2 className="h-4 w-4" /> {f}</li>
                ))}
              </ul>
              <a href={BRAND.whatsappHref} className={`mt-6 inline-flex items-center justify-center rounded-2xl bg-${BRAND.primary} px-4 py-2 font-semibold text-black hover:brightness-95`}>
                Pedir cotización
              </a>
            </div>
          ))}
        </div>
      </Container>
    </section>
  );
}

function Coverage() {
  return (
    <section className="py-16 sm:py-20">
      <Container>
        <SectionTitle eyebrow="Cobertura" title="¿Dónde operamos?" subtitle="Recolección y entrega en tu ciudad y alrededores" />
        <div className="mt-8 overflow-hidden rounded-3xl border shadow-sm">
          {/* Reemplaza el src del iframe con tu ubicación exacta */}
          <iframe
            title="Mapa de cobertura"
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d997343.2963772862!2d-74.437!3d4.65!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x8e3f9a3e5930ddbf%3A0x63f78072b7aeb!2sColombia!5e0!3m2!1ses!2sCO!4v1691794184211"
            className="h-[380px] w-full"
            loading="lazy"
            referrerPolicy="no-referrer-when-downgrade"
          />
        </div>
        <p className="mt-3 text-center text-sm text-gray-600">Personaliza el mapa con tu ciudad y zonas de cobertura.</p>
      </Container>
    </section>
  );
}

function FAQ() {
  const faqs = [
    { q: "¿Qué peso máximo reciben?", a: "Hasta 8 kg por envío estándar. Para cargas mayores, pregúntanos por WhatsApp." },
    { q: "¿Cómo pago?", a: "Efectivo, transferencia o contraentrega. Para empresa: factura mensual." },
    { q: "¿Tienen seguro?", a: "Sí, contamos con cobertura básica. Consulta condiciones según el tipo de envío." },
  ];
  return (
    <section className="bg-gray-50 py-16 sm:py-20">
      <Container>
        <SectionTitle eyebrow="FAQ" title="Preguntas frecuentes" />
        <div className="mx-auto mt-8 max-w-3xl divide-y rounded-3xl border bg-white">
          {faqs.map((f, i) => (
            <details key={f.q} className="group p-6">
              <summary className="flex cursor-pointer list-none items-center justify-between text-left text-base font-semibold text-gray-900">
                {f.q}
                <ChevronRight className="h-5 w-5 transition group-open:rotate-90" />
              </summary>
              <p className="mt-2 text-sm text-gray-700">{f.a}</p>
            </details>
          ))}
        </div>
      </Container>
    </section>
  );
}

function Footer() {
  return (
    <footer className="border-t bg-white py-10">
      <Container>
        <div className="flex flex-col items-center justify-between gap-4 sm:flex-row">
          <p className="text-sm text-gray-600">© {new Date().getFullYear()} {BRAND.name}. Todos los derechos reservados.</p>
          <div className="flex items-center gap-3">
            <a href={BRAND.whatsappHref} className="inline-flex items-center gap-2 rounded-full border px-4 py-2 text-sm font-semibold text-gray-800">
              <MessageCircle className="h-4 w-4" /> WhatsApp
            </a>
            <a href={BRAND.phoneHref} className="inline-flex items-center gap-2 rounded-full border px-4 py-2 text-sm font-semibold text-gray-800">
              <Phone className="h-4 w-4" /> {BRAND.phone}
            </a>
          </div>
        </div>
      </Container>

      {/* Botón flotante de WhatsApp */}
      <a
        href={BRAND.whatsappHref}
        className={`fixed bottom-6 right-6 hidden sm:inline-flex h-14 w-14 items-center justify-center rounded-full bg-${BRAND.primary} shadow-lg hover:brightness-95`}
        aria-label="WhatsApp"
      >
        <MessageCircle className="h-6 w-6 text-black" />
      </a>
    <div className="mt-8 text-center text-xs text-gray-500">
  <a href="#politica-datos">Política de Tratamiento de Datos</a>
</div>
</footer>

<section id="politica-datos" className="bg-white py-12">
  <Container>
    <h2 className="text-xl font-bold text-gray-900 mb-4">Política de Tratamiento de Datos</h2>
    <p className="text-sm text-gray-700 leading-relaxed">
      Moto Style Mensajería informa que los datos personales suministrados por los usuarios (nombre, dirección, teléfonos y demás información de contacto) serán utilizados únicamente para coordinar la recogida y entrega de envíos, confirmar tarifas y disponibilidad, y contactar al remitente y destinatario cuando sea necesario para completar el servicio.
      <br /><br />
      No compartimos la información con terceros, excepto cuando la ley lo exija o sea indispensable para cumplir el servicio contratado.
      <br /><br />
      El usuario podrá en cualquier momento solicitar la actualización o eliminación de sus datos escribiendo al WhatsApp 318 331 1111.
      <br /><br />
      Al enviar información a través del formulario o por WhatsApp, el usuario declara que autoriza el tratamiento de sus datos bajo los términos aquí descritos.
    </p>
  </Container>
</section>
  );
}

export default function MotoStyleLanding() {
  return (
    <div className="min-h-screen scroll-smooth bg-white">
      {/* NAV */}
      <header className="sticky top-0 z-50 bg-white/80 backdrop-blur">
        <Container>
          <div className="flex items-center justify-between py-4">
            <div className="flex items-center gap-3">
              <MotoLogo variant="mark" className="h-9 w-9" />
              <span className="text-lg font-extrabold text-gray-900">{BRAND.name}</span>
            </div>
            <nav className="hidden gap-6 text-sm font-semibold text-gray-700 sm:flex">
              <a href="#servicios" className="hover:text-gray-900">Servicios</a>
              <a href="#precios" className="hover:text-gray-900">Precios</a>
              <a href="#cobertura" className="hover:text-gray-900">Cobertura</a>
              <a href="#contacto" className="hover:text-gray-900">Contacto</a>
            </nav>
            <PrimaryBtn href={BRAND.whatsappHref}>
              <MessageCircle className="h-5 w-5" /> Cotizar
            </PrimaryBtn>
          </div>
        </Container>
      </header>

      {/* HERO */}
      <section id="inicio">
        <Hero />
      </section>

      {/* SERVICES */}
      <section id="servicios">
        <Services />
      </section>

      {/* PRICING */}
      <section id="precios">
        <Pricing />
      </section>

      {/* COVERAGE */}
      <section id="cobertura">
        <Coverage />
      </section>

      {/* FAQ */}
      <section>
        <FAQ />
      </section>

      {/* CONTACT */}
      <section id="contacto" className="bg-gray-50 py-16 sm:py-20">
        <Container>
          <SectionTitle eyebrow="Contacto" title="¿Listo para enviar?" subtitle="Escríbenos y agenda tu recolección" />
          <div className="mx-auto mt-8 max-w-2xl rounded-3xl border bg-white p-6 shadow-sm">
            <form onSubmit={(e) => { e.preventDefault(); const fd = new FormData(e.currentTarget as HTMLFormElement); const nombreEntrega = String(fd.get("nombreEntrega") || ""); const telEntrega = String(fd.get("telEntrega") || ""); const recogerDireccion = String(fd.get("recogerDireccion") || ""); const esConjunto = String(fd.get("esConjunto") || "no") === "si"; const casaApto = String(fd.get("casaApto") || ""); const entregarDireccion = String(fd.get("entregarDireccion") || ""); const nombreRecibe = String(fd.get("nombreRecibe") || ""); const telRecibe = String(fd.get("telRecibe") || ""); let msg = `Hola, quiero solicitar un servicio de mensajería.

RECOGER EN: ${recogerDireccion}
Nombre de quien entrega: ${nombreEntrega}
Teléfono de quien entrega: ${telEntrega}`; if (esConjunto || casaApto) { msg += `
Conjunto cerrado: ${esConjunto ? "Sí" : "No"}${casaApto ? `, Casa/Apartamento: ${casaApto}` : ""}`; } msg += `

ENTREGAR EN: ${entregarDireccion}
Nombre de quien recibe: ${nombreRecibe}
Contacto de quien recibe: ${telRecibe}`; const url = `${BRAND.whatsappHref}?text=${encodeURIComponent(msg)}`; window.location.href = url; }}>
              <div className="grid gap-4 sm:grid-cols-2">
                <input name="recogerDireccion" required placeholder="Recoger en (dirección exacta)" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <input name="entregarDireccion" required placeholder="Entregar en (dirección exacta)" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <input name="nombreEntrega" required placeholder="Nombre de quien entrega" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <input name="telEntrega" required type="tel" inputMode="numeric" pattern="[0-9]{10}" title="Ingresa 10 dígitos (ej. 3183311111)" placeholder="Teléfono de quien entrega (10 dígitos)" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <select name="esConjunto" className="rounded-xl border px-4 py-3 outline-none focus:ring">
                  <option value="no">¿Es conjunto cerrado? No</option>
                  <option value="si">¿Es conjunto cerrado? Sí</option>
                </select>
                <input name="casaApto" placeholder="Casa o apartamento (si aplica)" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <input name="nombreRecibe" required placeholder="Nombre de quien recibe" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
                <input name="telRecibe" required type="tel" inputMode="numeric" pattern="[0-9]{10}" title="Ingresa 10 dígitos (ej. 3001234567)" placeholder="Número de contacto de quien recibe (10 dígitos)" className="rounded-xl border px-4 py-3 outline-none focus:ring" />
              </div>
              <div className="mt-6 flex items-center justify-between">
                <p className="text-sm text-gray-600">* Los teléfonos deben tener <strong>10 dígitos</strong>. Al enviar, se abrirá WhatsApp con tu solicitud lista para enviar.</p>
                <button type="submit" className={`inline-flex items-center justify-center rounded-2xl bg-${BRAND.primary} px-4 py-2 font-semibold text-black hover:brightness-95`}>
                  Enviar por WhatsApp
                </button>
              </div>
            </form>
          </div>
        </Container>
      </section>

      {/* BANNER MÓVIL FIJO */}
      <div className="sm:hidden fixed bottom-0 inset-x-0 z-50 bg-black/90 backdrop-blur border-t border-white/10 animate-bounce-slow">
        <div className="mx-auto max-w-6xl px-4 py-3 flex items-center justify-between gap-3">
          <span className="text-white text-sm font-semibold">¿Necesitas un mensajero ahora?</span>
          <a href={BRAND.whatsappHref} className={`inline-flex items-center gap-2 rounded-xl bg-${BRAND.primary} px-4 py-2 text-sm font-bold text-black animate-color-swap`}>
            <MessageCircle className="h-4 w-4" /> WhatsApp
          </a>
        </div>
      </div>

      {/* FOOTER */}
      <Footer />
    </div>
  );
}
