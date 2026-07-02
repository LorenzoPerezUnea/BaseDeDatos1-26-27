## Ejercicio 2: Plataforma de Streaming y Torneos de Videojuegos

### 1. Lista predefinida de requisitos

1. La plataforma permite a los jugadores crear perfiles y seguir a otros jugadores.
2. Los jugadores pueden transmitir en vivo sus partidas.
3. La plataforma registra torneos y partidas.
4. Los espectadores pueden enviar donaciones y comentarios en vivo.
5. Se pueden generar estadísticas de rendimiento por jugador y torneo.
6. Cada juego tiene diferentes categorías y modos de juego.
7. Los jugadores pueden formar equipos y participar en torneos.

---

### 2. Identificación de Entidades

* Jugador: usuario de la plataforma que transmite y participa en torneos.
* Perfil: datos personales y preferencias del jugador.
* Transmisión: sesión en vivo de un jugador.
* Torneo: evento competitivo organizado en la plataforma.
* Partida: juego individual dentro de un torneo.
* Juego: título disponible en la plataforma.
* Equipo: conjunto de jugadores que participan juntos en torneos.
* Donación: aporte monetario de espectadores.
* Comentario: mensaje enviado por espectadores durante transmisiones.

---

### 3. Identificación de Relaciones

* Jugador–Perfil: un jugador tiene un perfil (1:1).
* Jugador–Transmisión: un jugador puede tener muchas transmisiones (1:N).
* Jugador–Equipo: un jugador puede pertenecer a varios equipos (N:M).
* Equipo–Torneo: un equipo puede participar en muchos torneos (N:M).
* Partida–Torneo: un torneo tiene muchas partidas (1:N).
* Partida–Juego: una partida corresponde a un juego (N:1).
* Espectador–Donación: un espectador puede hacer muchas donaciones (1:N).
* Espectador–Comentario: un espectador puede escribir muchos comentarios (1:N).

---

### 4. Identificación de Atributos

| Entidad      | Atributos                                                    |
| -------------- | -------------------------------------------------------------- |
| Jugador      | idJugador, nickname, nivel, experiencia, email               |
| Perfil       | idPerfil, avatar, bio, preferencias, redesSociales           |
| Transmisión | idTransmision, titulo, fechaHora, duración, visualizaciones |
| Torneo       | idTorneo, nombre, fechaInicio, fechaFin, premios             |
| Partida      | idPartida, fechaHora, duracion, resultado                    |
| Juego        | idJuego, nombre, genero, plataforma                          |
| Equipo       | idEquipo, nombre, ranking                                    |
| Donación    | idDonacion, monto, fechaHora                                 |
| Comentario   | idComentario, contenido, fechaHora                           |

---

### 5. Jerarquías / Generalizaciones

* Usuario (generalización) puede ser Jugador o Espectador.
* Evento (generalización) puede ser Transmisión o Torneo.

