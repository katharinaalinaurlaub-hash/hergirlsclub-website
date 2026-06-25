// =============================================================================
//  HER GIRLS CLUB — main.js
// =============================================================================

document.addEventListener('DOMContentLoaded', () => {

  initNav();
  initReveal();
  initForms();
  renderFeaturedEvent();
  renderHomeUpcoming();
  renderHomePast();
  renderAllUpcoming();
  renderAllPast();

});

// ── Navigation ────────────────────────────────────────────────────────────────

function initNav() {
  const nav = document.getElementById('nav');
  const burger = document.getElementById('burger');
  const mobileMenu = document.getElementById('mobileMenu');

  // Scroll shadow
  window.addEventListener('scroll', () => {
    nav.classList.toggle('scrolled', window.scrollY > 20);
  }, { passive: true });

  // Mobile menu toggle
  if (burger && mobileMenu) {
    burger.addEventListener('click', () => {
      const isOpen = mobileMenu.classList.toggle('open');
      burger.setAttribute('aria-expanded', isOpen);
    });
    mobileMenu.querySelectorAll('a').forEach(a => {
      a.addEventListener('click', () => mobileMenu.classList.remove('open'));
    });
  }

  // Active nav link
  const page = window.location.pathname.split('/').pop() || 'index.html';
  document.querySelectorAll('.nav__links a, .nav__mobile a').forEach(link => {
    if (link.getAttribute('href') === page) link.classList.add('active');
  });
}

// ── Scroll reveal ─────────────────────────────────────────────────────────────

function initReveal() {
  const els = document.querySelectorAll('.reveal');
  if (!els.length) return;

  if (!('IntersectionObserver' in window)) {
    els.forEach(el => el.classList.add('visible'));
    return;
  }

  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

  els.forEach(el => obs.observe(el));
}

// ── Forms ─────────────────────────────────────────────────────────────────────

function initForms() {
  // Newsletter forms
  document.querySelectorAll('.newsletter-form').forEach(form => {
    form.addEventListener('submit', e => {
      e.preventDefault();
      const email = form.querySelector('input[type=email]')?.value?.trim();
      if (!email) return;
      // TODO: Replace with Mailchimp / Brevo embed action URL
      const msg = document.createElement('p');
      msg.style.cssText = 'color:var(--pink);font-weight:600;text-align:center;padding:0.5rem 0';
      msg.textContent = '✓ You\'re on the list — see you at the next event!';
      form.replaceWith(msg);
    });
  });

  // Contact form
  const contactForm = document.getElementById('contactForm');
  if (contactForm) {
    contactForm.addEventListener('submit', e => {
      e.preventDefault();
      // TODO: Connect to Netlify Forms (add data-netlify="true" to the form)
      // or Formspree (set action="https://formspree.io/f/YOUR_ID" method="POST")
      contactForm.innerHTML = `
        <div style="text-align:center;padding:3rem 0">
          <div style="font-size:2.5rem;margin-bottom:1rem">✉️</div>
          <h3 style="font-family:var(--font-serif);font-weight:900;margin-bottom:0.5rem">Message sent!</h3>
          <p style="color:var(--text-mid)">We'll be in touch soon. In the meantime — follow us on Instagram.</p>
          <a href="https://www.instagram.com/hergirlsclub.ch/" target="_blank" rel="noopener"
             class="btn btn--primary mt-md" style="margin-top:1.5rem">@hergirlsclub →</a>
        </div>`;
    });
  }
}

// ── Event data helpers ────────────────────────────────────────────────────────

function getUpcoming() {
  if (typeof EVENTS === 'undefined') return [];
  return EVENTS
    .filter(e => e.status === 'upcoming')
    .sort((a, b) => new Date(a.dateSort) - new Date(b.dateSort));
}

function getPast() {
  if (typeof EVENTS === 'undefined') return [];
  return EVENTS
    .filter(e => e.status === 'past')
    .sort((a, b) => new Date(b.dateSort) - new Date(a.dateSort));
}

// ── Card HTML builders ────────────────────────────────────────────────────────

function eventCardHTML(event) {
  const tagBg = event.status === 'upcoming'
    ? 'background:var(--red);color:var(--white)'
    : 'background:var(--pink);color:var(--red)';
  const tagText = event.status === 'upcoming' ? 'Upcoming' : 'Recap';

  const imageBg = event.image
    ? `url('${event.image}'), linear-gradient(135deg,#F9C8D5 0%,#F4AABF 100%)`
    : `linear-gradient(135deg,#F9C8D5 0%,#F4AABF 100%)`;

  const partnersHTML = event.partners?.length
    ? `<div class="event-card__partners">with <strong>${event.partners.join(', ')}</strong></div>`
    : '<div></div>';

  const ctaHTML = event.ticketUrl
    ? `<a href="${event.ticketUrl}" class="btn btn--primary btn--sm" target="_blank" rel="noopener">Get Tickets →</a>`
    : (event.status === 'upcoming'
        ? `<span style="font-size:0.78rem;color:var(--text-mid);font-weight:500">Link coming soon</span>`
        : `<span style="font-size:0.78rem;color:var(--text-mid);font-weight:500">Closed</span>`);

  return `
    <div class="event-card reveal">
      <div class="event-card__image" style="background-image:${imageBg}">
        <span class="tag" style="${tagBg}">${tagText}</span>
      </div>
      <div class="event-card__body">
        <div class="event-card__meta">
          <span>${event.date}</span>
          <span>${event.location}</span>
        </div>
        <div class="event-card__title">${event.title}</div>
        <div class="event-card__desc">${event.description}</div>
        <div class="event-card__footer">
          ${partnersHTML}
          ${ctaHTML}
        </div>
      </div>
    </div>`;
}

// ── Render functions ──────────────────────────────────────────────────────────

// Home: big featured event card
function renderFeaturedEvent() {
  const el = document.getElementById('featuredEvent');
  if (!el) return;

  const featured = (typeof EVENTS !== 'undefined')
    ? (EVENTS.find(e => e.featured && e.status === 'upcoming') || getUpcoming()[0])
    : null;

  if (!featured) {
    el.innerHTML = '<p class="text-muted text-center" style="padding:2rem 0">More events coming soon — follow us on Instagram for updates.</p>';
    return;
  }

  const imageBg = featured.image
    ? `url('${featured.image}'), linear-gradient(135deg,#F9C8D5 0%,#F4AABF 100%)`
    : `linear-gradient(135deg,#F9C8D5 0%,#F4AABF 100%)`;

  const ctaHTML = featured.ticketUrl
    ? `<a href="${featured.ticketUrl}" class="btn btn--primary btn--lg" target="_blank" rel="noopener">Get Tickets →</a>`
    : `<a href="events.html" class="btn btn--primary btn--lg">All events →</a>`;

  el.innerHTML = `
    <div class="event-featured reveal">
      <div class="event-featured__image" style="background-image:${imageBg}"></div>
      <div class="event-featured__body">
        <div class="event-featured__badge">Next Event</div>
        <div class="event-featured__title">${featured.title}</div>
        <div class="event-featured__meta">${featured.date} · ${featured.location}</div>
        <p class="event-featured__desc">${featured.description}</p>
        ${ctaHTML}
      </div>
    </div>`;

  // Re-observe new elements
  observeNewReveals(el);
}

// Home: up to 2 more upcoming (excluding the featured one)
function renderHomeUpcoming() {
  const el = document.getElementById('homeUpcoming');
  if (!el) return;
  const featuredId = (typeof EVENTS !== 'undefined')
    ? (EVENTS.find(e => e.featured && e.status === 'upcoming') || getUpcoming()[0])?.id
    : null;
  const events = getUpcoming().filter(e => e.id !== featuredId).slice(0, 2);
  if (!events.length) { el.closest('section')?.style && (el.closest('section').style.display = 'none'); return; }
  el.innerHTML = events.map(eventCardHTML).join('');
  observeNewReveals(el);
}

// Home: last 3 past events
function renderHomePast() {
  const el = document.getElementById('homePast');
  if (!el) return;
  const events = getPast().slice(0, 3);
  if (!events.length) { el.closest('section')?.style && (el.closest('section').style.display = 'none'); return; }
  el.innerHTML = events.map(eventCardHTML).join('');
  observeNewReveals(el);
}

// Events page: all upcoming
function renderAllUpcoming() {
  const el = document.getElementById('allUpcoming');
  if (!el) return;
  const events = getUpcoming();
  if (!events.length) {
    el.innerHTML = '<p class="text-muted text-center" style="grid-column:1/-1;padding:2rem 0">More events coming soon — follow us on Instagram!</p>';
    return;
  }
  el.innerHTML = events.map(eventCardHTML).join('');
  observeNewReveals(el);
}

// Events page: all past
function renderAllPast() {
  const el = document.getElementById('allPast');
  if (!el) return;
  const events = getPast();
  if (!events.length) {
    el.innerHTML = '<p class="text-muted text-center" style="grid-column:1/-1;padding:2rem 0">Events will appear here after they take place.</p>';
    return;
  }
  el.innerHTML = events.map(eventCardHTML).join('');
  observeNewReveals(el);
}

// Re-run IntersectionObserver on freshly injected .reveal elements
function observeNewReveals(parent) {
  if (!('IntersectionObserver' in window)) {
    parent.querySelectorAll('.reveal').forEach(el => el.classList.add('visible'));
    return;
  }
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -30px 0px' });
  parent.querySelectorAll('.reveal:not(.visible)').forEach(el => obs.observe(el));
}
