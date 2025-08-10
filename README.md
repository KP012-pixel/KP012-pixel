
<!-- Paste this into your README.md as raw HTML -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 220 140" width="440" height="280" aria-label="Climbing and waving figure">
  <!-- Background -->
  <rect width="100%" height="100%" fill="none"/>

  <!-- Wall (in front, on left) -->
  <rect x="0" y="40" width="60" height="80" rx="4" fill="#444"/>

  <!-- Ground shadow -->
  <ellipse cx="140" cy="125" rx="40" ry="6" fill="#000" opacity="0.08"/>

  <!-- Figure group (head, body, arm) -->
  <!-- initial transform places the figure partly behind the wall -->
  <g id="figure" transform="translate(10 90)">
    <!-- head -->
    <circle cx="20" cy="-28" r="8" fill="#f6c9a0" stroke="#333" stroke-width="1"/>
    <!-- body -->
    <rect x="16" y="-20" width="8" height="20" rx="3" fill="#2b7a78" stroke="#1f5b5a" />
    <!-- left leg -->
    <rect x="14" y="0" width="4" height="14" rx="2" fill="#1f5b5a"/>
    <!-- right leg -->
    <rect x="22" y="0" width="4" height="14" rx="2" fill="#1f5b5a"/>

    <!-- waving arm (right arm) - we rotate this around a pivot inside the group -->
    <g id="arm" transform="translate(28 -18)">
      <!-- arm shape (a thin rectangle) centered so rotation pivot is 6,6 -->
      <rect x="-6" y="-2" width="12" height="4" rx="2" fill="#f6c9a0" stroke="#333" stroke-width="0.6"/>
      <!-- hand -->
      <circle cx="6" cy="0" r="2.2" fill="#f6c9a0" stroke="#333" stroke-width="0.6"/>
    </g>
  </g>

  <!-- The climb animation: figure moves up (appears to climb behind the wall) -->
  <animateTransform
    xlink:href="#figure"
    attributeName="transform"
    type="translate"
    id="climb"
    values="10 90; 10 40"
    dur="1.6s"
    begin="0s"
    fill="freeze" />

  <!-- A short pause, then the jump: figure moves right and down (a little arc feel) -->
  <!-- Using a second translate to replace the transform -->
  <animateTransform
    xlink:href="#figure"
    attributeName="transform"
    type="translate"
    id="jump"
    values="10 40; 60 15; 120 95"
    keyTimes="0;0.45;1"
    dur="1.0s"
    begin="climb.end + 0.25s"
    calcMode="spline"
    keySplines="0.2 0.6 0.2 1; 0.3 0 0.1 1"
    fill="freeze" />

  <!-- Arm waving: rotate the arm group around its local pivot while the figure is settled -->
  <animateTransform
    xlink:href="#arm"
    attributeName="transform"
    type="rotate"
    values="0 0 0; -30 0 0; 25 0 0; -15 0 0; 0 0 0"
    dur="1.1s"
    begin="jump.begin + 0.2s"
    repeatCount="3"
    fill="freeze" />

  <!-- Optional tiny bounce when landing -->
  <animateTransform
    xlink:href="#figure"
    attributeName="transform"
    type="translate"
    values="120 95; 120 90; 120 95"
    keyTimes="0;0.4;1"
    dur="0.45s"
    begin="jump.end"
    fill="freeze" />

</svg>