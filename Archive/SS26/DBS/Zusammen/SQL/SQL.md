```mySQL
--
-- PostgreSQL database dump
--

SET statement_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SET check_function_bodies = false;
SET client_min_messages = warning;

--
-- Name: plpgsql; Type: EXTENSION; Schema: -; Owner: 
--

CREATE EXTENSION IF NOT EXISTS plpgsql WITH SCHEMA pg_catalog;


--
-- Name: EXTENSION plpgsql; Type: COMMENT; Schema: -; Owner: 
--

COMMENT ON EXTENSION plpgsql IS 'PL/pgSQL procedural language';


SET search_path = public, pg_catalog;

SET default_tablespace = '';

SET default_with_oids = false;

--
-- Name: assistant; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE assistant (
    empid integer NOT NULL,
    name character varying(30) NOT NULL,
    area character varying(30),
    boss integer
);


ALTER TABLE public.assistant OWNER TO postgres;

--
-- Name: course; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE course (
    courseid integer NOT NULL,
    title character varying(30),
    ects integer,
    taughtby integer
);


ALTER TABLE public.course OWNER TO postgres;

--
-- Name: grades; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE grades (
    studid integer NOT NULL,
    courseid integer NOT NULL,
    empid integer NOT NULL,
    grade numeric(2,1),
    CONSTRAINT grades_grade_check CHECK (((grade >= 0.7) AND (grade <= 5.0)))
);


ALTER TABLE public.grades OWNER TO postgres;

--
-- Name: professor; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE professor (
    empid integer NOT NULL,
    name character varying(30) NOT NULL,
    rank character(2),
    office integer NOT NULL,
    CONSTRAINT professor_rank_check CHECK ((rank = ANY (ARRAY['C2'::bpchar, 'C3'::bpchar, 'C4'::bpchar])))
);


ALTER TABLE public.professor OWNER TO postgres;

--
-- Name: requires; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE requires (
    predecessor integer NOT NULL,
    successor integer NOT NULL
);


ALTER TABLE public.requires OWNER TO postgres;

--
-- Name: student; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE student (
    studid integer NOT NULL,
    name character varying(30) NOT NULL,
    semester integer
);


ALTER TABLE public.student OWNER TO postgres;

--
-- Name: takes; Type: TABLE; Schema: public; Owner: postgres; Tablespace: 
--

CREATE TABLE takes (
    studid integer NOT NULL,
    courseid integer NOT NULL
);


ALTER TABLE public.takes OWNER TO postgres;

--
-- Name: test; Type: VIEW; Schema: public; Owner: postgres
--

CREATE VIEW test AS
    SELECT grades.studid, grades.courseid, grades.empid, grades.grade FROM grades;


ALTER TABLE public.test OWNER TO postgres;

--
-- Data for Name: assistant; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY assistant (empid, name, area, boss) FROM stdin;
3002	Platon	Ideology	2125
3003	Aristoteles	Syllogistics	2125
3004	Wittgenstein	Language Theory	2126
3005	Rhetikus	Planetary Motion	2127
3006	Newton	Kepler's laws	2127
3007	Spinoza	God and Nature	2134
\.

--
-- Data for Name: course; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY course (courseid, title, ects, taughtby) FROM stdin;
5001	Basics	4	2137
5041	Ethics	4	2125
5043	Theory of Cognition	3	2126
5049	DBS	2	2125
4052	Logics	4	2125
5052	Theory of Science	3	2126
5216	Bioethics	2	2126
5259	Advanced Algorithms	2	2133
5022	Belief and Knowledge	2	2134
4630	Constructive Criticism	4	2137
\.


--
-- Data for Name: grades; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY grades (studid, courseid, empid, grade) FROM stdin;
28106	5001	2126	1.0
25403	5041	2125	2.0
27550	4630	2137	2.0
\.


--
-- Data for Name: professor; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY professor (empid, name, rank, office) FROM stdin;
2125	Socrates	C4	226
2126	Russel	C4	232
2127	Kopernikus	C3	310
2133	Popper	C3	52
2134	Augustinus	C3	309
2136	Curie	C4	36
2137	Kant	C4	7
\.


--
-- Data for Name: requires; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY requires (predecessor, successor) FROM stdin;
5001	5041
5001	5043
5001	5049
5041	5216
5043	5052
5041	5052
5052	5259
\.


--
-- Data for Name: student; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY student (studid, name, semester) FROM stdin;
24002	Xenokrates	18
25403	Jonas	12
26120	Fichte	10
26830	Aristoxenos	8
27550	Schopenhauer	6
28106	Carnap	3
29120	Theophrastos	2
29555	Feuerbach	2
\.


--
-- Data for Name: takes; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY takes (studid, courseid) FROM stdin;
26120	5001
27550	5001
27550	4052
28106	5041
28106	5052
28106	5216
28106	5259
29120	5001
29120	5041
29120	5049
29555	5022
25403	5022
29555	5001
\.


--
-- Name: assistant_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY assistant
    ADD CONSTRAINT assistant_pkey PRIMARY KEY (empid);


--
-- Name: course_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY course
    ADD CONSTRAINT course_pkey PRIMARY KEY (courseid);


--
-- Name: grades_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY grades
    ADD CONSTRAINT grades_pkey PRIMARY KEY (studid, courseid);


--
-- Name: professor_office_key; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY professor
    ADD CONSTRAINT professor_office_key UNIQUE (office);


--
-- Name: professor_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY professor
    ADD CONSTRAINT professor_pkey PRIMARY KEY (empid);


--
-- Name: requires_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY requires
    ADD CONSTRAINT requires_pkey PRIMARY KEY (predecessor, successor);


--
-- Name: student_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY student
    ADD CONSTRAINT student_pkey PRIMARY KEY (studid);


--
-- Name: takes_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres; Tablespace: 
--

ALTER TABLE ONLY takes
    ADD CONSTRAINT takes_pkey PRIMARY KEY (studid, courseid);


--
-- Name: pk; Type: INDEX; Schema: public; Owner: postgres; Tablespace: 
--

CREATE INDEX pk ON assistant USING btree (empid);

ALTER TABLE assistant CLUSTER ON pk;


--
-- Name: prof index; Type: INDEX; Schema: public; Owner: postgres; Tablespace: 
--

CREATE INDEX "prof index" ON professor USING btree (empid, name);

ALTER TABLE professor CLUSTER ON "prof index";


--
-- Name: assistant_boss_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY assistant
    ADD CONSTRAINT assistant_boss_fkey FOREIGN KEY (boss) REFERENCES professor(empid);


--
-- Name: course_taughtby_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY course
    ADD CONSTRAINT course_taughtby_fkey FOREIGN KEY (taughtby) REFERENCES professor(empid);


--
-- Name: grades_courseid_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY grades
    ADD CONSTRAINT grades_courseid_fkey FOREIGN KEY (courseid) REFERENCES course(courseid);


--
-- Name: grades_empid_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY grades
    ADD CONSTRAINT grades_empid_fkey FOREIGN KEY (empid) REFERENCES professor(empid);


--
-- Name: grades_studid_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY grades
    ADD CONSTRAINT grades_studid_fkey FOREIGN KEY (studid) REFERENCES student(studid) ON DELETE CASCADE;


--
-- Name: requires_predecessor_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--
 ALTER TABLE ONLY requires
    ADD CONSTRAINT requires_predecessor_fkey FOREIGN KEY (predecessor) REFERENCES course(courseid) ON DELETE CASCADE;


--
-- Name: requires_successor_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY requires
    ADD CONSTRAINT requires_successor_fkey FOREIGN KEY (successor) REFERENCES course(courseid) ON DELETE CASCADE;


--
-- Name: takes_courseid_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY takes
    ADD CONSTRAINT takes_courseid_fkey FOREIGN KEY (courseid) REFERENCES course(courseid) ON DELETE CASCADE;


--
-- Name: takes_studid_fkey; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY takes
    ADD CONSTRAINT takes_studid_fkey FOREIGN KEY (studid) REFERENCES student(studid) ON DELETE CASCADE;


--
-- Name: public; Type: ACL; Schema: -; Owner: postgres
--

REVOKE ALL ON SCHEMA public FROM PUBLIC;
REVOKE ALL ON SCHEMA public FROM postgres;
GRANT ALL ON SCHEMA public TO postgres;
GRANT ALL ON SCHEMA public TO PUBLIC;


--
-- PostgreSQL database dump complete
```