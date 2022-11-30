CREATE TABLE IF NOT EXISTS janre (
	id SERIAL PRIMARY KEY,
	janre_name VARCHAR(40) UNIQUE NOT NULL
);
	
CREATE TABLE IF NOT EXISTS performer (
	id SERIAL PRIMARY KEY,
	performer_name VARCHAR(300) UNIQUE NOT NULL
);

CREATE TABLE IF NOT EXISTS album (
	id SERIAL PRIMARY KEY,
	album_name VARCHAR(300) UNIQUE NOT NULL,
	release_year VARCHAR(4) NOT NULL
);

CREATE TABLE IF NOT EXISTS track (
	id SERIAL PRIMARY KEY,
	track_name VARCHAR(200) UNIQUE NOT NULL,
	track_length VARCHAR(15) NOT NULL,
	album_id INTEGER NOT NULL REFERENCES album(id)
);

CREATE TABLE IF NOT EXISTS digest (
	id SERIAL PRIMARY KEY,
	digest_name VARCHAR(300) UNIQUE NOT NULL,
	release_year VARCHAR(4) NOT NULL
);

CREATE TABLE IF NOT EXISTS performers_in_janres (
	janre_id INTEGER REFERENCES janre(id),
	performer_id INTEGER REFERENCES performer(id),
	CONSTRAINT pk PRIMARY KEY (janre_id, performer_id)
);

CREATE TABLE IF NOT EXISTS performers_albums (
	performer_id INTEGER REFERENCES performer(id),
	album_id INTEGER REFERENCES album(id),
	CONSTRAINT pk1 PRIMARY KEY (performer_id, album_id)
);

CREATE TABLE IF NOT EXISTS tracks_in_digests (
	track_id INTEGER REFERENCES track(id),
	digest_id INTEGER REFERENCES digest(id),
	CONSTRAINT pk2 PRIMARY KEY (track_id, digest_id)
);